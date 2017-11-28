---
title: "Parámetros de entrada de runbook | Microsoft Docs"
description: "Los parámetros de entrada de Runbook aumentan la flexibilidad de los Runbooks porque permiten pasar datos a un Runbook cuando se inicia. En este artículo se describen los distintos escenarios donde se usan parámetros de entrada en Runbooks."
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
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="b04dd-104">Parámetros de entrada de Runbook</span><span class="sxs-lookup"><span data-stu-id="b04dd-104">Runbook input parameters</span></span>
<span data-ttu-id="b04dd-105">Los parámetros de entrada de Runbook aumentan la flexibilidad de los Runbooks porque permiten pasarle datos cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="b04dd-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="b04dd-106">Los parámetros permiten dirigir acciones de Runbook a entornos y escenarios específicos.</span><span class="sxs-lookup"><span data-stu-id="b04dd-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="b04dd-107">En este artículo, le guiaremos por los distintos escenarios donde se usan parámetros de entrada en Runbooks.</span><span class="sxs-lookup"><span data-stu-id="b04dd-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="b04dd-108">Configuración de parámetros de entrada</span><span class="sxs-lookup"><span data-stu-id="b04dd-108">Configure input parameters</span></span>
<span data-ttu-id="b04dd-109">Los parámetros de entrada pueden configurarse en Runbooks gráficos, de PowerShell y de flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b04dd-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="b04dd-110">Un Runbook puede tener varios parámetros con tipos de datos diferentes o sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="b04dd-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="b04dd-111">Los parámetros de entrada pueden ser obligatorios u opcionales, y puede asignar un valor predeterminado a los parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="b04dd-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="b04dd-112">Puede asignar valores a los parámetros de entrada para un Runbook cuando lo inicia mediante uno de los métodos disponibles.</span><span class="sxs-lookup"><span data-stu-id="b04dd-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="b04dd-113">Entre estos métodos, se incluye iniciar un Runbook mediante el portal o un servicio web.</span><span class="sxs-lookup"><span data-stu-id="b04dd-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="b04dd-114">También puede iniciarlo como Runbook secundario al que se llama insertado en otro Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="b04dd-115">Configuración de parámetros de entrada en Runbooks de PowerShell y de flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b04dd-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="b04dd-116">Los Runbooks de PowerShell y de [flujo de trabajo de PowerShell](automation-first-runbook-textual.md) en Automatización de Azure admiten parámetros de entrada que se definen mediante los siguientes atributos.</span><span class="sxs-lookup"><span data-stu-id="b04dd-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="b04dd-117">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="b04dd-117">**Property**</span></span> | <span data-ttu-id="b04dd-118">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="b04dd-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="b04dd-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="b04dd-119">Type</span></span> |<span data-ttu-id="b04dd-120">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="b04dd-120">Required.</span></span> <span data-ttu-id="b04dd-121">Tipo de datos previsto para el valor del parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="b04dd-122">Es válido cualquier tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="b04dd-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="b04dd-123">Nombre</span><span class="sxs-lookup"><span data-stu-id="b04dd-123">Name</span></span> |<span data-ttu-id="b04dd-124">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="b04dd-124">Required.</span></span> <span data-ttu-id="b04dd-125">El nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-125">The name of the parameter.</span></span> <span data-ttu-id="b04dd-126">Debe ser único dentro del Runbook y puede contener solo letras, números o caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="b04dd-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="b04dd-127">Debe empezar por una letra.</span><span class="sxs-lookup"><span data-stu-id="b04dd-127">It must start with a letter.</span></span> |
| <span data-ttu-id="b04dd-128">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b04dd-128">Mandatory</span></span> |<span data-ttu-id="b04dd-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-129">Optional.</span></span> <span data-ttu-id="b04dd-130">Especifica si se debe proporcionar un valor para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="b04dd-131">Si se establece en **$true**, se debe proporcionar un valor cuando se inicia el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="b04dd-132">Si se establece en **$false**, el valor es opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="b04dd-133">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="b04dd-133">Default value</span></span> |<span data-ttu-id="b04dd-134">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-134">Optional.</span></span>  <span data-ttu-id="b04dd-135">Especifica un valor que se usará para el parámetro si no se pasa un valor al iniciar el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="b04dd-136">Se puede establecer un valor predeterminado para cualquier parámetro y hará automáticamente que el parámetro sea opcional independientemente de la configuración de Mandatory.</span><span class="sxs-lookup"><span data-stu-id="b04dd-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="b04dd-137">Windows PowerShell admite más atributos de parámetros de entrada de los enumerados aquí, como validación, alias y conjuntos de parámetros.</span><span class="sxs-lookup"><span data-stu-id="b04dd-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="b04dd-138">Sin embargo, Automatización de Azure actualmente solo admite los parámetros de entrada enumerados antes.</span><span class="sxs-lookup"><span data-stu-id="b04dd-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="b04dd-139">Una definición de parámetro en los Runbooks de flujo de trabajo de PowerShell tiene el formato general siguiente, donde los distintos parámetros están separados por comas.</span><span class="sxs-lookup"><span data-stu-id="b04dd-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="b04dd-140">Al definir parámetros, si no se especifica el atributo **Mandatory** , el parámetro se considera opcional de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b04dd-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="b04dd-141">Además, si se establece un valor predeterminado para un parámetro en Runbooks de flujo de trabajo de PowerShell, PowerShell lo tratará como un parámetro opcional, independientemente del valor del atributo **Mandatory**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="b04dd-142">Por ejemplo, vamos a configurar los parámetros de entrada para un Runbook de flujo de trabajo de PowerShell que proporciona detalles sobre las máquinas virtuales, una o varias, de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b04dd-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="b04dd-143">Este Runbook tiene dos parámetros, como se muestra en la siguiente captura de pantalla: el nombre de la máquina virtual y el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b04dd-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![Automatización, flujo de trabajo de PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="b04dd-145">En esta definición de parámetros, los parámetros **$VMName** y **$resourceGroupName** son parámetros simples de tipo String.</span><span class="sxs-lookup"><span data-stu-id="b04dd-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="b04dd-146">Sin embargo, los Runbooks de PowerShell y de flujo de trabajo de PowerShell admiten todos los tipos simples y complejos, como **object** o **PSCredential**, como parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="b04dd-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="b04dd-147">Si el Runbook tiene un parámetro de entrada de tipo object, use una tabla hash de PowerShell con pares (nombre,valor) para pasar un valor.</span><span class="sxs-lookup"><span data-stu-id="b04dd-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="b04dd-148">Por ejemplo, si tiene el siguiente parámetro en un Runbook:</span><span class="sxs-lookup"><span data-stu-id="b04dd-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="b04dd-149">Puede pasar el siguiente valor al parámetro:</span><span class="sxs-lookup"><span data-stu-id="b04dd-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="b04dd-150">Configuración de parámetros de entrada en Runbooks gráficos</span><span class="sxs-lookup"><span data-stu-id="b04dd-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="b04dd-151">Para [configurar un Runbook gráfico](automation-first-runbook-graphical.md) con parámetros de entrada, vamos a crear un Runbook gráfico que proporciona detalles sobre las máquinas virtuales, una o varias, de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b04dd-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="b04dd-152">La configuración de un Runbook consta de dos actividades principales, como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="b04dd-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="b04dd-153">[**Autenticación de Runbooks con una cuenta de ejecución de Azure**](automation-sec-configure-azure-runas-account.md) para autenticarse con Azure.</span><span class="sxs-lookup"><span data-stu-id="b04dd-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="b04dd-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) para obtener las propiedades de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b04dd-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="b04dd-155">Puede usar la actividad [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) para obtener los nombres de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b04dd-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="b04dd-156">La actividad **Get AzureRmVm** acepta dos parámetros, el **nombre de máquina virtual** y el **nombre del grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="b04dd-157">Puesto que estos parámetros requieren valores diferentes cada vez que se inicia el Runbook, puede agregar parámetros de entrada a su Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="b04dd-158">Estos son los pasos para agregar parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="b04dd-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="b04dd-159">Seleccione el Runbook gráfico de la hoja **Runbooks** y [**edítelo**](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b04dd-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="b04dd-160">En el editor de Runbooks, haga clic en **Entrada y salida** para abrir la hoja **Entrada y salida**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![Runbook gráfico de Automatización](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="b04dd-162">La hoja **Entrada y salida** muestra una lista de parámetros de entrada definidos para el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="b04dd-163">En esta hoja, puede agregar un nuevo parámetro de entrada o editar la configuración de uno existente.</span><span class="sxs-lookup"><span data-stu-id="b04dd-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="b04dd-164">Para agregar un nuevo parámetro para el Runbook, haga clic en **Agregar entrada** para abrir la hoja **Parámetro de entrada de Runbook**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="b04dd-165">En ella puede configurar los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="b04dd-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="b04dd-166">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="b04dd-166">**Property**</span></span> | <span data-ttu-id="b04dd-167">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="b04dd-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b04dd-168">Nombre</span><span class="sxs-lookup"><span data-stu-id="b04dd-168">Name</span></span> |<span data-ttu-id="b04dd-169">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="b04dd-169">Required.</span></span>  <span data-ttu-id="b04dd-170">El nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-170">The name of the parameter.</span></span> <span data-ttu-id="b04dd-171">Debe ser único dentro del Runbook y puede contener solo letras, números o caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="b04dd-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="b04dd-172">Debe empezar por una letra.</span><span class="sxs-lookup"><span data-stu-id="b04dd-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="b04dd-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="b04dd-173">Description</span></span> |<span data-ttu-id="b04dd-174">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-174">Optional.</span></span> <span data-ttu-id="b04dd-175">Descripción del propósito del parámetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="b04dd-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="b04dd-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="b04dd-176">Type</span></span> |<span data-ttu-id="b04dd-177">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-177">Optional.</span></span> <span data-ttu-id="b04dd-178">Tipo de datos previsto para el valor del parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="b04dd-179">Los tipos de parámetro admitidos son **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** y **Object**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="b04dd-180">Si no se selecciona ningún tipo de datos, el valor predeterminado es **String**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="b04dd-181">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b04dd-181">Mandatory</span></span> |<span data-ttu-id="b04dd-182">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-182">Optional.</span></span> <span data-ttu-id="b04dd-183">Especifica si se debe proporcionar un valor para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="b04dd-184">Si elige **yes**, se debe proporcionar un valor cuando se inicia el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="b04dd-185">Si elige **no**, no se necesita un valor cuando se inicia el Runbook y se puede establecer un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="b04dd-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="b04dd-186">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="b04dd-186">Default Value</span></span> |<span data-ttu-id="b04dd-187">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-187">Optional.</span></span> <span data-ttu-id="b04dd-188">Especifica un valor que se usará para el parámetro si no se pasa un valor al iniciar el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="b04dd-189">Puede establecerse un valor predeterminado para un parámetro que no sea obligatorio.</span><span class="sxs-lookup"><span data-stu-id="b04dd-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="b04dd-190">Para establecer un valor predeterminado, elija **Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="b04dd-191">Este valor se usa a menos que se proporcione otro valor al iniciar el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="b04dd-192">Elija **Ninguno** si no desea proporcionar ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="b04dd-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![Agregar nueva entrada](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="b04dd-194">Cree dos parámetros con las siguientes propiedades que usará la actividad **Get-AzureRmVm**:</span><span class="sxs-lookup"><span data-stu-id="b04dd-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="b04dd-195">**Parameter1:**</span><span class="sxs-lookup"><span data-stu-id="b04dd-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="b04dd-196">Nombre: VMName</span><span class="sxs-lookup"><span data-stu-id="b04dd-196">Name - VMName</span></span>
     * <span data-ttu-id="b04dd-197">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b04dd-197">Type - String</span></span>
     * <span data-ttu-id="b04dd-198">Obligatorio: No</span><span class="sxs-lookup"><span data-stu-id="b04dd-198">Mandatory - No</span></span>
   * <span data-ttu-id="b04dd-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="b04dd-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="b04dd-200">Nombre: resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b04dd-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="b04dd-201">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="b04dd-201">Type - String</span></span>
     * <span data-ttu-id="b04dd-202">Obligatorio: No</span><span class="sxs-lookup"><span data-stu-id="b04dd-202">Mandatory - No</span></span>
     * <span data-ttu-id="b04dd-203">Valor predeterminado: Personalizado</span><span class="sxs-lookup"><span data-stu-id="b04dd-203">Default value - Custom</span></span>
     * <span data-ttu-id="b04dd-204">Valor predeterminado personalizado: \<Nombre del grupo de recursos que contiene las máquinas virtuales></span><span class="sxs-lookup"><span data-stu-id="b04dd-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="b04dd-205">Una vez agregados los parámetros, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="b04dd-206">Ahora puede verlos en la **hoja Entrada y salida**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="b04dd-207">Haga clic en **Aceptar** de nuevo y después en **Guardar** y en **Publicar** para publicar el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="b04dd-208">Asignación de valores a parámetros de entrada en Runbooks</span><span class="sxs-lookup"><span data-stu-id="b04dd-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="b04dd-209">Puede pasar valores a parámetros de entrada en Runbooks en los siguientes escenarios.</span><span class="sxs-lookup"><span data-stu-id="b04dd-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="b04dd-210">Inicio de un Runbook y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="b04dd-211">Se puede iniciar un Runbook de muchas maneras: mediante Azure Portal, con un webhook, con cmdlets de PowerShell, con la API de REST o con el SDK.</span><span class="sxs-lookup"><span data-stu-id="b04dd-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="b04dd-212">A continuación, se describen distintos métodos para iniciar un Runbook y asignar parámetros.</span><span class="sxs-lookup"><span data-stu-id="b04dd-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="b04dd-213">Inicio de un Runbook publicado mediante el Portal de Azure y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="b04dd-214">Cuando se [inicia el Runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), se abre la hoja **Iniciar runbook** y puede configurar los valores para los parámetros que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="b04dd-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![Empezar a usar el portal](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="b04dd-216">En la etiqueta bajo el cuadro de entrada, puede ver los atributos que se han definido para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="b04dd-217">Entre los atributos, se incluye si es obligatorio u opcional, el tipo y el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="b04dd-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="b04dd-218">En el globo de ayuda junto al nombre del parámetro puede ver toda la información importante que necesita para tomar decisiones acerca de los valores de entrada de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="b04dd-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="b04dd-219">Esta información incluye si un parámetro es obligatorio u opcional.</span><span class="sxs-lookup"><span data-stu-id="b04dd-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="b04dd-220">También incluye el tipo y el valor predeterminado (si existe), además de otras notas útiles.</span><span class="sxs-lookup"><span data-stu-id="b04dd-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![Globo de ayuda](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="b04dd-222">Los parámetros de tipo String admiten valores de cadena **Empty** .</span><span class="sxs-lookup"><span data-stu-id="b04dd-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="b04dd-223">Si escribe **[EmptyString]** en el cuadro del parámetro de entrada, pasará una cadena vacía al parámetro.</span><span class="sxs-lookup"><span data-stu-id="b04dd-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="b04dd-224">Además, los parámetros de tipo String no permiten que se pasen valores **Null** .</span><span class="sxs-lookup"><span data-stu-id="b04dd-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="b04dd-225">Si no pasa ningún valor al parámetro de tipo String, PowerShell lo interpretará como Null.</span><span class="sxs-lookup"><span data-stu-id="b04dd-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="b04dd-226">Inicio de un Runbook publicado mediante cmdlets de PowerShell y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="b04dd-227">**Cmdlets de Azure Resource Manager:** puede iniciar un Runbook de automatización creado en un grupo de recursos mediante [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04dd-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="b04dd-228">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="b04dd-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="b04dd-229">**Cmdlets de Administración de servicios de Azure:** puede iniciar un Runbook de automatización creado en un grupo de recursos predeterminado mediante [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04dd-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="b04dd-230">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="b04dd-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="b04dd-231">Cuando se inicia un Runbook mediante cmdlets de PowerShell, se crea un parámetro predeterminado, **MicrosoftApplicationManagementStartedBy**, con el valor **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b04dd-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="b04dd-232">Puede ver este parámetro en la hoja **Detalles del trabajo** .</span><span class="sxs-lookup"><span data-stu-id="b04dd-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="b04dd-233">Inicio de un Runbook con un SDK y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="b04dd-234">**Método Azure Resource Manager:** puede iniciar un Runbook mediante el SDK de un lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="b04dd-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="b04dd-235">A continuación, se muestra un fragmento de código C# para iniciar un Runbook en su cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="b04dd-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="b04dd-236">Puede ver todo el código en nuestro [repositorio de GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="b04dd-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="b04dd-237">**Método Administración de servicios de Azure:** puede iniciar un Runbook mediante el SDK de un lenguaje de programación.</span><span class="sxs-lookup"><span data-stu-id="b04dd-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="b04dd-238">A continuación, se muestra un fragmento de código C# para iniciar un Runbook en su cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="b04dd-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="b04dd-239">Puede ver todo el código en nuestro [repositorio de GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="b04dd-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="b04dd-240">Para iniciar este método, cree un diccionario para almacenar los parámetros del Runbook, **VMName** y **resourceGroupName**, así como sus valores.</span><span class="sxs-lookup"><span data-stu-id="b04dd-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="b04dd-241">A continuación, inicie el Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-241">Then start the runbook.</span></span> <span data-ttu-id="b04dd-242">A continuación, se muestra el fragmento de código C# para llamar al método definido más arriba.</span><span class="sxs-lookup"><span data-stu-id="b04dd-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="b04dd-243">Inicio de un Runbook con la API de REST y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="b04dd-244">Se puede crear un trabajo de Runbook e iniciarlo con la API de REST de Automatización de Azure usando el método **PUT** con el siguiente identificador URI de solicitud.</span><span class="sxs-lookup"><span data-stu-id="b04dd-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="b04dd-245">En el identificador URI de solicitud, reemplace los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="b04dd-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="b04dd-246">**subscription-id** : identificador de su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="b04dd-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="b04dd-247">**cloud-service-name:** nombre del servicio en la nube al que se debe enviar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b04dd-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="b04dd-248">**automation-account-name:** nombre de la cuenta de automatización hospedada en el servicio en la nube especificado.</span><span class="sxs-lookup"><span data-stu-id="b04dd-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="b04dd-249">**job-id:** GUID del trabajo.</span><span class="sxs-lookup"><span data-stu-id="b04dd-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="b04dd-250">En PowerShell, los GUID pueden crearse con el comando **[GUID]::NewGuid().ToString()** .</span><span class="sxs-lookup"><span data-stu-id="b04dd-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="b04dd-251">Para pasar parámetros al trabajo de Runbook, use el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b04dd-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="b04dd-252">Admite las dos propiedades siguientes proporcionadas en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="b04dd-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="b04dd-253">**Nombre del Runbook**: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="b04dd-253">**Runbook name:** Required.</span></span> <span data-ttu-id="b04dd-254">El nombre del Runbook para que se inicie el trabajo.</span><span class="sxs-lookup"><span data-stu-id="b04dd-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="b04dd-255">**Parámetros del Runbook**: opcionales.</span><span class="sxs-lookup"><span data-stu-id="b04dd-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="b04dd-256">Diccionario de la lista de parámetros en formato (nombre, valor), donde el nombre debe ser de tipo String y el valor puede ser cualquier valor JSON válido.</span><span class="sxs-lookup"><span data-stu-id="b04dd-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="b04dd-257">Si desea iniciar el Runbook **Get-AzureVMTextual** creado antes con **VMName** y **resourceGroupName** como parámetros, use el siguiente formato JSON para el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b04dd-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

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

<span data-ttu-id="b04dd-258">Si el trabajo se crea correctamente, se devuelve un código de estado HTTP 201.</span><span class="sxs-lookup"><span data-stu-id="b04dd-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="b04dd-259">Para más información sobre los encabezados y el cuerpo de la respuesta, consulte el artículo acerca de cómo [crear un trabajo de Runbook mediante la API de REST](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="b04dd-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="b04dd-260">Prueba de un Runbook y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="b04dd-261">Cuando se [prueba la versión de borrador del Runbook](automation-testing-runbook.md) mediante la opción de prueba, se abre la hoja **Prueba** y puede configurar los valores de los parámetros recién creados.</span><span class="sxs-lookup"><span data-stu-id="b04dd-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![Prueba y asignación de parámetros](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="b04dd-263">Vinculación de una programación a un Runbook y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="b04dd-264">También puede [vincular una programación](automation-schedules.md) a su Runbook para que este se inicie en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="b04dd-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="b04dd-265">Asigne los parámetros de entrada al crear la programación y el Runbook los usará cuando se inicie mediante la programación.</span><span class="sxs-lookup"><span data-stu-id="b04dd-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="b04dd-266">No se puede guardar la programación hasta que se proporcionen todos los valores de los parámetros obligatorios.</span><span class="sxs-lookup"><span data-stu-id="b04dd-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![Programación y asignación de parámetros](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="b04dd-268">Creación de un Webhook para un Runbook y asignación de parámetros</span><span class="sxs-lookup"><span data-stu-id="b04dd-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="b04dd-269">Puede crear un [Webhook](automation-webhooks.md) para el Runbook y configurar los parámetros de entrada del Runbook.</span><span class="sxs-lookup"><span data-stu-id="b04dd-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="b04dd-270">No se puede guardar el Webhook hasta que se proporcionen todos los valores de los parámetros obligatorios.</span><span class="sxs-lookup"><span data-stu-id="b04dd-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Creación de un Webhook y asignación de parámetros](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="b04dd-272">Cuando se ejecuta un Runbook mediante un webhook, se envía un parámetro de entrada predefinido **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** , junto con los parámetros de entrada que definió.</span><span class="sxs-lookup"><span data-stu-id="b04dd-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="b04dd-273">Puede hacer clic para expandir el parámetro **WebhookData** para más detalles.</span><span class="sxs-lookup"><span data-stu-id="b04dd-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![Parámetro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="b04dd-275">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b04dd-275">Next steps</span></span>
* <span data-ttu-id="b04dd-276">Para más información sobre la entrada y salida de Runbooks, consulte [Azure Automation: Runbook Input, Output, and Nested Runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)(Automatización de Azure: entrada y salida de Runbooks, y Runbooks anidados).</span><span class="sxs-lookup"><span data-stu-id="b04dd-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="b04dd-277">Para más información acerca de diferentes maneras de iniciar un Runbook, consulte [Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b04dd-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="b04dd-278">Para editar un Runbook de texto, consulte [Edición de runbooks de texto en Automatización de Azure](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b04dd-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="b04dd-279">Para editar un Runbook gráfico, consulte [Creación gráfica en Automatización de Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b04dd-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

