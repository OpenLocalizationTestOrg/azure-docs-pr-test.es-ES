---
title: "parámetros de entrada de aaaRunbook | Documentos de Microsoft"
description: "Parámetros de entrada de runbook aumentan la flexibilidad de Hola de runbooks permitiéndole toopass datos tooa runbook cuando se inicia. En este artículo se describen los distintos escenarios donde se usan parámetros de entrada en Runbooks."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="09e13-104">Parámetros de entrada de Runbook</span><span class="sxs-lookup"><span data-stu-id="09e13-104">Runbook input parameters</span></span>
<span data-ttu-id="09e13-105">Parámetros de entrada de runbook aumentan la flexibilidad de Hola de runbooks permitiéndole toopass datos tooit cuando se inicie.</span><span class="sxs-lookup"><span data-stu-id="09e13-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="09e13-106">los parámetros de Hello permiten Hola runbook acciones toobe destinado a entornos y escenarios concretos.</span><span class="sxs-lookup"><span data-stu-id="09e13-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="09e13-107">En este artículo, le guiaremos por los distintos escenarios donde se usan parámetros de entrada en Runbooks.</span><span class="sxs-lookup"><span data-stu-id="09e13-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="09e13-108">Configuración de parámetros de entrada</span><span class="sxs-lookup"><span data-stu-id="09e13-108">Configure input parameters</span></span>
<span data-ttu-id="09e13-109">Los parámetros de entrada pueden configurarse en Runbooks gráficos, de PowerShell y de flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09e13-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="09e13-110">Un Runbook puede tener varios parámetros con tipos de datos diferentes o sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="09e13-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="09e13-111">Los parámetros de entrada pueden ser obligatorios u opcionales, y puede asignar un valor predeterminado a los parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="09e13-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="09e13-112">Puede asignar valores de parámetros de entrada de toohello para un runbook cuando se inicia a través de uno de los métodos disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="09e13-113">Estos métodos incluyen iniciar un runbook desde el portal de Hola o un servicio web.</span><span class="sxs-lookup"><span data-stu-id="09e13-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="09e13-114">También puede iniciarlo como Runbook secundario al que se llama insertado en otro Runbook.</span><span class="sxs-lookup"><span data-stu-id="09e13-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="09e13-115">Configuración de parámetros de entrada en Runbooks de PowerShell y de flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="09e13-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="09e13-116">PowerShell y [runbooks de flujo de trabajo de PowerShell](automation-first-runbook-textual.md) en automatización de Azure admite parámetros de entrada que se definen a través de los siguientes atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="09e13-117">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="09e13-117">**Property**</span></span> | <span data-ttu-id="09e13-118">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="09e13-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="09e13-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="09e13-119">Type</span></span> |<span data-ttu-id="09e13-120">Necesario.</span><span class="sxs-lookup"><span data-stu-id="09e13-120">Required.</span></span> <span data-ttu-id="09e13-121">tipo de datos de Hello esperado para el valor del parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="09e13-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="09e13-122">Es válido cualquier tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="09e13-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="09e13-123">Nombre</span><span class="sxs-lookup"><span data-stu-id="09e13-123">Name</span></span> |<span data-ttu-id="09e13-124">Necesario.</span><span class="sxs-lookup"><span data-stu-id="09e13-124">Required.</span></span> <span data-ttu-id="09e13-125">nombre de Hello del parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="09e13-125">hello name of hello parameter.</span></span> <span data-ttu-id="09e13-126">Esto debe ser único dentro de runbook de hello y pueden contener solo letras, números o caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="09e13-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="09e13-127">Debe empezar por una letra.</span><span class="sxs-lookup"><span data-stu-id="09e13-127">It must start with a letter.</span></span> |
| <span data-ttu-id="09e13-128">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="09e13-128">Mandatory</span></span> |<span data-ttu-id="09e13-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-129">Optional.</span></span> <span data-ttu-id="09e13-130">Especifica si se debe proporcionar un valor para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="09e13-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="09e13-131">Si se establece demasiado**$true**, a continuación, se debe proporcionar un valor al iniciar runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="09e13-132">Si se establece demasiado**$false**, a continuación, un valor es opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="09e13-133">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="09e13-133">Default value</span></span> |<span data-ttu-id="09e13-134">Opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-134">Optional.</span></span>  <span data-ttu-id="09e13-135">Especifica un valor que se usará para el parámetro hello si no se pasa un valor de cuando se inicie el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="09e13-136">Un valor predeterminado se puede establecer para cualquier parámetro y realizará automáticamente parámetro hello opcional independientemente Hola parámetro obligatorio.</span><span class="sxs-lookup"><span data-stu-id="09e13-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="09e13-137">Windows PowerShell admite más atributos de parámetros de entrada de los enumerados aquí, como validación, alias y conjuntos de parámetros.</span><span class="sxs-lookup"><span data-stu-id="09e13-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="09e13-138">Sin embargo, automatización de Azure admite actualmente solo Hola parámetros de entrada mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="09e13-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="09e13-139">Una definición de parámetro en los runbooks de flujo de trabajo de PowerShell tiene Hola después de forma general, donde varios parámetros se separan por comas.</span><span class="sxs-lookup"><span data-stu-id="09e13-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="09e13-140">Si va a definir parámetros, si no se especifica hello **obligatorio** atributo, de forma predeterminada, el parámetro hello se considera opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="09e13-141">Además, si establece un valor predeterminado para un parámetro en los runbooks de flujo de trabajo de PowerShell, se tratará PowerShell como un parámetro opcional, con independencia de hello **obligatorio** valor de atributo.</span><span class="sxs-lookup"><span data-stu-id="09e13-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="09e13-142">Por ejemplo, vamos a configurar los parámetros de entrada de hello en un runbook de flujo de trabajo de PowerShell que proporciona detalles sobre las máquinas virtuales, una sola máquina virtual o todas las máquinas virtuales dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09e13-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="09e13-143">Este runbook tiene dos parámetros, como se muestra en la siguiente captura de pantalla de Hola: nombre de Hola de máquina virtual y el nombre de Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09e13-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![Automatización, flujo de trabajo de PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="09e13-145">En esta definición de parámetro, Hola parámetros **$VMName** y **$resourceGroupName** son simples parámetros de tipo cadena.</span><span class="sxs-lookup"><span data-stu-id="09e13-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="09e13-146">Sin embargo, los Runbooks de PowerShell y de flujo de trabajo de PowerShell admiten todos los tipos simples y complejos, como **object** o **PSCredential**, como parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="09e13-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="09e13-147">Si el runbook tiene un parámetro de entrada de tipo de objeto, a continuación, utilice una tabla hash de PowerShell por (nombre, valor) pares toopass en un valor.</span><span class="sxs-lookup"><span data-stu-id="09e13-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="09e13-148">Por ejemplo, si tienes Hola después de parámetro en un runbook:</span><span class="sxs-lookup"><span data-stu-id="09e13-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="09e13-149">A continuación, puede pasar Hola siguiendo el valor del parámetro toohello:</span><span class="sxs-lookup"><span data-stu-id="09e13-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="09e13-150">Configuración de parámetros de entrada en Runbooks gráficos</span><span class="sxs-lookup"><span data-stu-id="09e13-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="09e13-151">demasiado[configurar un runbook gráfico](automation-first-runbook-graphical.md) con parámetros de entrada, vamos a crear un runbook gráfico que muestra detalles acerca de las máquinas virtuales, ya sea una sola máquina virtual o todas las máquinas virtuales dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09e13-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="09e13-152">La configuración de un Runbook consta de dos actividades principales, como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="09e13-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="09e13-153">[**Autenticar Runbooks con la cuenta de identificación de Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate con Azure.</span><span class="sxs-lookup"><span data-stu-id="09e13-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="09e13-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget propiedades de Hola de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="09e13-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="09e13-155">Puede usar hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nombres de actividad toooutput Hola de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="09e13-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="09e13-156">Hola actividad **Get AzureRmVm** acepta dos parámetros, hello **nombre de máquina virtual** hello y **nombre del grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="09e13-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="09e13-157">Puesto que estos parámetros requieren valores diferentes cada vez que inicie runbook hello, puede agregar parámetros de entrada tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="09e13-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="09e13-158">Estos son parámetros de entrada tooadd Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="09e13-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="09e13-159">Seleccione Hola runbook gráfico de hello **Runbooks** hoja y, a continuación, haga clic en [ **editar** ](automation-graphical-authoring-intro.md) lo.</span><span class="sxs-lookup"><span data-stu-id="09e13-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="09e13-160">En el editor de runbook hello, haga clic en **de entrada y salida** tooopen hello **de entrada y salida** hoja.</span><span class="sxs-lookup"><span data-stu-id="09e13-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Runbook gráfico de Automatización](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="09e13-162">Hola **de entrada y salida** hoja muestra una lista de parámetros de entrada que se definen para el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="09e13-163">En esta hoja, puede agregar un nuevo parámetro de entrada o editar configuración de Hola de un parámetro de entrada existente.</span><span class="sxs-lookup"><span data-stu-id="09e13-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="09e13-164">tooadd un nuevo parámetro hello runbook, haga clic en **Agregar entrada** tooopen hello **parámetro de entrada de Runbook** hoja.</span><span class="sxs-lookup"><span data-stu-id="09e13-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="09e13-165">Allí, puede configurar Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="09e13-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="09e13-166">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="09e13-166">**Property**</span></span> | <span data-ttu-id="09e13-167">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="09e13-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="09e13-168">Nombre</span><span class="sxs-lookup"><span data-stu-id="09e13-168">Name</span></span> |<span data-ttu-id="09e13-169">Necesario.</span><span class="sxs-lookup"><span data-stu-id="09e13-169">Required.</span></span>  <span data-ttu-id="09e13-170">nombre de Hello del parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="09e13-170">hello name of hello parameter.</span></span> <span data-ttu-id="09e13-171">Esto debe ser único dentro de runbook de hello y pueden contener solo letras, números o caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="09e13-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="09e13-172">Debe empezar por una letra.</span><span class="sxs-lookup"><span data-stu-id="09e13-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="09e13-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="09e13-173">Description</span></span> |<span data-ttu-id="09e13-174">Opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-174">Optional.</span></span> <span data-ttu-id="09e13-175">Descripción sobre el propósito de hello del parámetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="09e13-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="09e13-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="09e13-176">Type</span></span> |<span data-ttu-id="09e13-177">Opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-177">Optional.</span></span> <span data-ttu-id="09e13-178">tipo de datos de Hola que se espera que el valor del parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="09e13-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="09e13-179">Los tipos de parámetro admitidos son **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** y **Object**.</span><span class="sxs-lookup"><span data-stu-id="09e13-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="09e13-180">Si no se selecciona un tipo de datos, el valor predeterminado es demasiado**cadena**.</span><span class="sxs-lookup"><span data-stu-id="09e13-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="09e13-181">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="09e13-181">Mandatory</span></span> |<span data-ttu-id="09e13-182">Opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-182">Optional.</span></span> <span data-ttu-id="09e13-183">Especifica si se debe proporcionar un valor para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="09e13-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="09e13-184">Si elige **Sí**, a continuación, se debe proporcionar un valor al iniciar runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="09e13-185">Si elige **no**, a continuación, no se requiere un valor cuando se inicie el runbook de Hola y puede establecerse un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="09e13-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="09e13-186">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="09e13-186">Default Value</span></span> |<span data-ttu-id="09e13-187">Opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-187">Optional.</span></span> <span data-ttu-id="09e13-188">Especifica un valor que se usará para el parámetro hello si no se pasa un valor de cuando se inicie el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="09e13-189">Puede establecerse un valor predeterminado para un parámetro que no sea obligatorio.</span><span class="sxs-lookup"><span data-stu-id="09e13-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="09e13-190">Elija un valor predeterminado, tooset **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="09e13-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="09e13-191">Este valor se utiliza a menos que se proporcione otro valor cuando se inicie el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="09e13-192">Elija **ninguno** si no desea que tooprovide cualquier valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="09e13-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Agregar nueva entrada](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="09e13-194">Crear dos parámetros con propiedades que se va a utilizar Hola siguientes de hello **AzureRmVm Get** actividad:</span><span class="sxs-lookup"><span data-stu-id="09e13-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="09e13-195">**Parameter1:**</span><span class="sxs-lookup"><span data-stu-id="09e13-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="09e13-196">Nombre: VMName</span><span class="sxs-lookup"><span data-stu-id="09e13-196">Name - VMName</span></span>
     * <span data-ttu-id="09e13-197">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="09e13-197">Type - String</span></span>
     * <span data-ttu-id="09e13-198">Obligatorio: No</span><span class="sxs-lookup"><span data-stu-id="09e13-198">Mandatory - No</span></span>
   * <span data-ttu-id="09e13-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="09e13-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="09e13-200">Nombre: resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="09e13-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="09e13-201">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="09e13-201">Type - String</span></span>
     * <span data-ttu-id="09e13-202">Obligatorio: No</span><span class="sxs-lookup"><span data-stu-id="09e13-202">Mandatory - No</span></span>
     * <span data-ttu-id="09e13-203">Valor predeterminado: Personalizado</span><span class="sxs-lookup"><span data-stu-id="09e13-203">Default value - Custom</span></span>
     * <span data-ttu-id="09e13-204">Valor predeterminado personalizado - \<nombre del grupo de recursos de Hola que contiene máquinas virtuales de hello ></span><span class="sxs-lookup"><span data-stu-id="09e13-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="09e13-205">Una vez que agregue parámetros hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="09e13-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="09e13-206">Ahora puede ver en hello **entrada y el módulo de salida**.</span><span class="sxs-lookup"><span data-stu-id="09e13-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="09e13-207">Haga clic en **Aceptar** de nuevo y después en **Guardar** y en **Publicar** para publicar el Runbook.</span><span class="sxs-lookup"><span data-stu-id="09e13-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="09e13-208">Asignar valores tooinput parámetros en runbooks</span><span class="sxs-lookup"><span data-stu-id="09e13-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="09e13-209">Puede pasar valores tooinput parámetros en runbooks en hello los escenarios siguientes.</span><span class="sxs-lookup"><span data-stu-id="09e13-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="09e13-210">Inicio de un Runbook y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="09e13-211">Se puede iniciar un runbook muchas maneras: a través del portal de Azure, con un webhook, con los cmdlets de PowerShell, con hello API de REST o con hello SDK Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="09e13-212">A continuación, se describen distintos métodos para iniciar un Runbook y asignar parámetros.</span><span class="sxs-lookup"><span data-stu-id="09e13-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="09e13-213">Iniciar un runbook publicado mediante Hola portal de Azure y asignar parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="09e13-214">Cuando se [iniciar runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **iniciar Runbook** hoja se abre y puede configurar valores para parámetros de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="09e13-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Empezar a usar el portal de Hola](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="09e13-216">En etiqueta de hello debajo del cuadro de entrada de hello, puede ver los atributos de Hola que se han configurado para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="09e13-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="09e13-217">Entre los atributos, se incluye si es obligatorio u opcional, el tipo y el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="09e13-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="09e13-218">En hello ayuda globo siguiente toohello nombre del parámetro, puede ver toda información de clave de hello necesita toomake decisiones acerca de los valores de entrada de parámetro.</span><span class="sxs-lookup"><span data-stu-id="09e13-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="09e13-219">Esta información incluye si un parámetro es obligatorio u opcional.</span><span class="sxs-lookup"><span data-stu-id="09e13-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="09e13-220">También incluye el tipo de Hola y valor predeterminado (si existe) y otras notas útiles.</span><span class="sxs-lookup"><span data-stu-id="09e13-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Globo de ayuda](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="09e13-222">Los parámetros de tipo String admiten valores de cadena **Empty** .</span><span class="sxs-lookup"><span data-stu-id="09e13-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="09e13-223">Escriba **[EmptyString]** en el parámetro de entrada de hello cuadro pasará un parámetro de toohello de cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="09e13-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="09e13-224">Además, los parámetros de tipo String no permiten que se pasen valores **Null** .</span><span class="sxs-lookup"><span data-stu-id="09e13-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="09e13-225">Si no pasa ningún parámetro de cadena de valor toohello, a continuación, PowerShell interpretará esa como null.</span><span class="sxs-lookup"><span data-stu-id="09e13-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="09e13-226">Inicio de un Runbook publicado mediante cmdlets de PowerShell y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="09e13-227">**Cmdlets de Azure Resource Manager:** puede iniciar un Runbook de automatización creado en un grupo de recursos mediante [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="09e13-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="09e13-228">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="09e13-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="09e13-229">**Cmdlets de Administración de servicios de Azure:** puede iniciar un Runbook de automatización creado en un grupo de recursos predeterminado mediante [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="09e13-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="09e13-230">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="09e13-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="09e13-231">Cuando se inicia un runbook mediante cmdlets de PowerShell, un parámetro predeterminado, **MicrosoftApplicationManagementStartedBy** se crea con el valor de hello **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="09e13-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="09e13-232">Puede ver este parámetro en hello **detalles del trabajo** hoja.</span><span class="sxs-lookup"><span data-stu-id="09e13-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="09e13-233">Inicio de un Runbook con un SDK y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="09e13-234">**Método de administrador de recursos de Azure:** pueden iniciar un runbook mediante Hola SDK de un lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="09e13-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="09e13-235">A continuación, se muestra un fragmento de código C# para iniciar un Runbook en su cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="09e13-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="09e13-236">Puede ver todo el código de hello en nuestro [repositorio de GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="09e13-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="09e13-237">**Método de administración de servicios de Azure:** pueden iniciar un runbook mediante Hola SDK de un lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="09e13-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="09e13-238">A continuación, se muestra un fragmento de código C# para iniciar un Runbook en su cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="09e13-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="09e13-239">Puede ver todo el código de hello en nuestro [repositorio de GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="09e13-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="09e13-240">toostart este método, crear un hello toostore de diccionario de parámetros de runbook, **VMName** y **resourceGroupName**y sus valores.</span><span class="sxs-lookup"><span data-stu-id="09e13-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="09e13-241">A continuación, inicie runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-241">Then start hello runbook.</span></span> <span data-ttu-id="09e13-242">A continuación se muestra hello C# fragmento de código para llamar al método hello definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="09e13-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="09e13-243">Iniciar un runbook mediante la API de REST de Hola y asignar parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="09e13-244">Se puede crear un trabajo de runbook e inició con hello API de REST de automatización de Azure mediante hello **colocar** método con hello siguiente URI de solicitud.</span><span class="sxs-lookup"><span data-stu-id="09e13-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="09e13-245">Hola URI de la solicitud, reemplace Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="09e13-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="09e13-246">**subscription-id** : identificador de su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="09e13-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="09e13-247">**nombre del servicio de nube:** se debe enviar el nombre de Hola de solicitud de hello en la nube servicio toowhich Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="09e13-248">**nombre de cuenta de automatización:** nombre de Hola de su cuenta de automatización que se hospeda dentro de hello especifica el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="09e13-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="09e13-249">**Id. de trabajo:** Hola GUID para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="09e13-250">Se pueden crear GUID en PowerShell mediante el uso de hello **[GUID]::NewGuid(). ToString()** comando.</span><span class="sxs-lookup"><span data-stu-id="09e13-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="09e13-251">En el trabajo de runbook de orden toopass parámetros toohello, utilice el cuerpo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="09e13-252">Toma Hola dos propiedades que se proporcionan en formato JSON siguientes:</span><span class="sxs-lookup"><span data-stu-id="09e13-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="09e13-253">**Nombre del Runbook**: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="09e13-253">**Runbook name:** Required.</span></span> <span data-ttu-id="09e13-254">nombre de Hola de runbook de Hola para hello toostart de trabajo.</span><span class="sxs-lookup"><span data-stu-id="09e13-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="09e13-255">**Parámetros del Runbook**: opcionales.</span><span class="sxs-lookup"><span data-stu-id="09e13-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="09e13-256">Dar formato a un diccionario de la lista de parámetros hello (nombre, valor) donde el nombre debe ser de tipo cadena y valor puede ser cualquier valor JSON válido.</span><span class="sxs-lookup"><span data-stu-id="09e13-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="09e13-257">Si desea que hello toostart **Get AzureVMTextual** runbook que creó anteriormente con **VMName** y **resourceGroupName** como parámetros, use Hola siguiendo el formato JSON en el cuerpo de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="09e13-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="09e13-258">Si se creó correctamente el trabajo de hello, se devuelve un código de estado HTTP 201.</span><span class="sxs-lookup"><span data-stu-id="09e13-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="09e13-259">Para obtener más información sobre encabezados de respuesta y el cuerpo de respuesta de hello, consulte el artículo toohello acerca de cómo demasiado[crear un trabajo de runbook mediante Hola API de REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="09e13-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="09e13-260">Prueba de un Runbook y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="09e13-261">Cuando se [versión de borrador de Hola de prueba del runbook](automation-testing-runbook.md) mediante la opción de prueba de hello, Hola **probar** hoja se abre y puede configurar valores para parámetros de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="09e13-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Prueba y asignación de parámetros](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="09e13-263">Vincular un runbook de tooa de programación y asignar parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="09e13-264">También puede [vincular una programación](automation-schedules.md) tooyour runbook para ese runbook Hola se inicia en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="09e13-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="09e13-265">Asignar parámetros de entrada cuando se crean Hola y Hola runbook usará estos valores cuando se inicia según la programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e13-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="09e13-266">No se puede guardar la programación de hello hasta que se proporcionan todos los valores de parámetro obligatorio.</span><span class="sxs-lookup"><span data-stu-id="09e13-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Programación y asignación de parámetros](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="09e13-268">Creación de un Webhook para un Runbook y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="09e13-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="09e13-269">Puede crear un [Webhook](automation-webhooks.md) para el Runbook y configurar los parámetros de entrada del Runbook.</span><span class="sxs-lookup"><span data-stu-id="09e13-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="09e13-270">No se puede guardar hello webhook hasta que se proporcionan todos los valores de parámetro obligatorio.</span><span class="sxs-lookup"><span data-stu-id="09e13-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Creación de un Webhook y asignación de parámetros](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="09e13-272">Cuando se ejecuta un runbook mediante el uso de un webhook, Hola predefinidos de parámetro de entrada  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  se envía junto con los parámetros de entrada de Hola que ha definido.</span><span class="sxs-lookup"><span data-stu-id="09e13-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="09e13-273">Puede hacer clic en hello tooexpand **WebhookData** parámetro para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="09e13-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![Parámetro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="09e13-275">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09e13-275">Next steps</span></span>
* <span data-ttu-id="09e13-276">Para más información sobre la entrada y salida de Runbooks, consulte [Azure Automation: Runbook Input, Output, and Nested Runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)(Automatización de Azure: entrada y salida de Runbooks, y Runbooks anidados).</span><span class="sxs-lookup"><span data-stu-id="09e13-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="09e13-277">Para obtener más información acerca de diferentes maneras toostart un runbook, consulte [a partir de un runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="09e13-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="09e13-278">tooedit un runbook textual, consulte demasiado[editar runbooks textuales](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="09e13-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="09e13-279">tooedit un runbook gráfico, consulte demasiado[edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="09e13-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

