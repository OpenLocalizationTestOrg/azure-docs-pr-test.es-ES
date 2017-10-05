---
title: Recursos de variables en Azure Automation | Microsoft Docs
description: "Los activos de variables son valores que están disponibles para todos los runbooks y configuraciones de DSC en Automatización de Azure.  En este artículo se explican los detalles de las variables y cómo trabajar con ellas en la creación de texto y gráficos."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="87e28-104">Recursos de variables en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="87e28-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="87e28-105">Los activos de variables son valores que están disponibles para todos los runbooks y configuraciones de DSC en su cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="87e28-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="87e28-106">Pueden crearse, modificarse y recuperarse desde el Portal de Azure, Windows PowerShell y desde un runbook o una configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="87e28-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="87e28-107">Las variables de Automatización son útiles para los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="87e28-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="87e28-108">Compartir un valor entre varios runbooks o configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="87e28-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="87e28-109">Compartir un valor entre varios trabajos del mismo runbook o configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="87e28-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="87e28-110">Administrar un valor desde el portal o desde la línea de comandos de Windows PowerShell que usan los runbooks, o bien las configuraciones DSC, como un conjunto de elementos de configuración comunes, como una lista específica de nombres de VM, un grupo de recursos específico, un nombre de dominio de AD, etc.</span><span class="sxs-lookup"><span data-stu-id="87e28-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="87e28-111">Las variables de Automatización se conservan para que sigan estando disponibles, incluso si se produce un error en el runbook o la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="87e28-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="87e28-112">Esto también permite que se establezca un valor por un runbook que se usará por otro o bien se usará por el mismo runbook o configuración de DSC la siguiente vez que se ejecute.</span><span class="sxs-lookup"><span data-stu-id="87e28-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="87e28-113">Cuando se crea una variable, puede especificar que se almacene cifrada.</span><span class="sxs-lookup"><span data-stu-id="87e28-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="87e28-114">Cuando se cifra una variable, se almacena de forma segura en Azure Automation y su valor no se puede recuperar del cmdlet [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) que se incluye como parte del módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87e28-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="87e28-115">Es la única manera de que se puede recuperar un valor cifrado desde la actividad **Get-AutomationVariable** en un runbook o una configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="87e28-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="87e28-116">Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas.</span><span class="sxs-lookup"><span data-stu-id="87e28-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="87e28-117">Estos recursos se cifran y se almacenan en Automatización de Azure con una clave única que se genera para cada cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="87e28-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="87e28-118">Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="87e28-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="87e28-119">Antes de almacenar un recurso seguro, la clave de la cuenta de automatización se descifra con el certificado maestro y, a continuación, se utiliza para cifrar el recurso.</span><span class="sxs-lookup"><span data-stu-id="87e28-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="87e28-120">Tipos de variables</span><span class="sxs-lookup"><span data-stu-id="87e28-120">Variable types</span></span>

<span data-ttu-id="87e28-121">Cuando se crea una variable con el portal de Azure, debe especificar un tipo de datos en la lista desplegable para que el portal pueda mostrar el control adecuado para escribir el valor de la variable.</span><span class="sxs-lookup"><span data-stu-id="87e28-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="87e28-122">La variable no se limita a este tipo de datos, pero hay que establecer la variable mediante Windows PowerShell si se desea especificar un valor de un tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="87e28-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="87e28-123">Si especifica **No definido**, el valor de la variable se establecerá en **$null** y deberá establecer el valor con el cmdlet [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) o con la actividad **Set-AutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="87e28-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="87e28-124">No se puede crear o cambiar el valor de un tipo complejo de variable en el portal, pero puede proporcionar un valor de cualquier tipo mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87e28-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="87e28-125">Los tipos complejos se devolverán como un [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="87e28-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="87e28-126">Puede almacenar varios valores en una única variable mediante la creación de una matriz o tabla hash y guardarlos en la variable.</span><span class="sxs-lookup"><span data-stu-id="87e28-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="87e28-127">La siguiente es una lista de los tipos de variables disponibles en Automation:</span><span class="sxs-lookup"><span data-stu-id="87e28-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="87e28-128">Cadena</span><span class="sxs-lookup"><span data-stu-id="87e28-128">String</span></span>
* <span data-ttu-id="87e28-129">Entero </span><span class="sxs-lookup"><span data-stu-id="87e28-129">Integer</span></span>
* <span data-ttu-id="87e28-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="87e28-130">DateTime</span></span>
* <span data-ttu-id="87e28-131">Booleano</span><span class="sxs-lookup"><span data-stu-id="87e28-131">Boolean</span></span>
* <span data-ttu-id="87e28-132">Null</span><span class="sxs-lookup"><span data-stu-id="87e28-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="87e28-133">Cmdlets y actividades de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="87e28-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="87e28-134">Los cmdlets de la tabla siguiente se usan para crear y administrar variables de Automatización con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87e28-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="87e28-135">Se incluyen como parte del [módulo Azure PowerShell](../powershell-install-configure.md) que está disponible para su uso en los runbooks de Automatización y las configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="87e28-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="87e28-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="87e28-136">Cmdlets</span></span>|<span data-ttu-id="87e28-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="87e28-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="87e28-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="87e28-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="87e28-139">Recupera el valor de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="87e28-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="87e28-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="87e28-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="87e28-141">Crea una nueva variable y establece su valor.</span><span class="sxs-lookup"><span data-stu-id="87e28-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="87e28-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="87e28-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="87e28-143">Quita una variable existente.</span><span class="sxs-lookup"><span data-stu-id="87e28-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="87e28-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="87e28-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="87e28-145">Establece el valor de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="87e28-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="87e28-146">Las actividades de flujo de trabajo en la tabla siguiente se usan para acceder a las variables de Automatización en un runbook.</span><span class="sxs-lookup"><span data-stu-id="87e28-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="87e28-147">Solo están disponibles para su uso en un runbook o una configuración de DSC y no se incluyen como parte del módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87e28-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="87e28-148">Actividades de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="87e28-148">Workflow Activities</span></span>|<span data-ttu-id="87e28-149">Description</span><span class="sxs-lookup"><span data-stu-id="87e28-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="87e28-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="87e28-150">Get-AutomationVariable</span></span>|<span data-ttu-id="87e28-151">Recupera el valor de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="87e28-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="87e28-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="87e28-152">Set-AutomationVariable</span></span>|<span data-ttu-id="87e28-153">Establece el valor de una variable existente.</span><span class="sxs-lookup"><span data-stu-id="87e28-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="87e28-154">Debe evitar el uso de variables en el parámetro – Name de **Get-AutomationVariable** en un runbook o una configuración de DSC, ya que puede complicar la detección de dependencias entre runbooks o configuraciones de DSC y las variables de Automation en tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="87e28-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="87e28-155">Creación de una nueva variable de Automatización</span><span class="sxs-lookup"><span data-stu-id="87e28-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="87e28-156">Para crear una nueva variable con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="87e28-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="87e28-157">En la cuenta de Automation, haga clic en el icono **Activos** y, en la hoja **Activos**, seleccione **Variables**.</span><span class="sxs-lookup"><span data-stu-id="87e28-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="87e28-158">En la hoja **Variables**, seleccione **Agregar una variable**.</span><span class="sxs-lookup"><span data-stu-id="87e28-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="87e28-159">Complete las opciones en la hoja **Nueva variable** y haga clic en **Crear** para guardar la nueva variable.</span><span class="sxs-lookup"><span data-stu-id="87e28-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="87e28-160">Para crear una nueva variable con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="87e28-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="87e28-161">El cmdlet [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) crea una nueva variable y establece su valor inicial.</span><span class="sxs-lookup"><span data-stu-id="87e28-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="87e28-162">Puede recuperar el valor mediante [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="87e28-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="87e28-163">Si el valor es un tipo simple, se devuelve ese mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="87e28-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="87e28-164">Si es un tipo complejo, se devuelve **PSCustomObject** .</span><span class="sxs-lookup"><span data-stu-id="87e28-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="87e28-165">Los comandos de ejemplo siguientes muestran cómo crear una variable de tipo cadena y que después devuelva su valor.</span><span class="sxs-lookup"><span data-stu-id="87e28-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="87e28-166">Los comandos de ejemplo siguientes muestran cómo crear una variable con un tipo complejo y que después devuelva su valor.</span><span class="sxs-lookup"><span data-stu-id="87e28-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="87e28-167">En este caso, se usa un objeto de máquina virtual desde **Get-AzureRmVm**.</span><span class="sxs-lookup"><span data-stu-id="87e28-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="87e28-168">Uso de una variable en un runbook o una configuración de DSC</span><span class="sxs-lookup"><span data-stu-id="87e28-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="87e28-169">Use la actividad **Set-AutomationVariable** para establecer el valor de una variable de Automation en un runbook o una configuración de DSC y **Get-AutomationVariable** para recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="87e28-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="87e28-170">No debe usar los cmdlets **Set-AzureAutomationVariable** o **Get-AzureAutomationVariable** en un runbook o una configuración DSC, ya que son menos eficientes que las actividades de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="87e28-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="87e28-171">Tampoco puede recuperar el valor de variables seguras con **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="87e28-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="87e28-172">La única forma de crear una nueva variable desde un runbook o una configuración de DSC es usar el cmdlet [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx).</span><span class="sxs-lookup"><span data-stu-id="87e28-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="87e28-173">Ejemplos de runbook textual</span><span class="sxs-lookup"><span data-stu-id="87e28-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="87e28-174">Establecimiento y recuperación de un valor simple de una variable</span><span class="sxs-lookup"><span data-stu-id="87e28-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="87e28-175">Los comandos de ejemplo siguientes muestran cómo establecer y recuperar una variable en un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="87e28-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="87e28-176">En este ejemplo, se asume que se crearon las variables de tipo entero llamadas *NumberOfIterations* y *NumberOfRunnings* y una variable de tipo cadena denominada *SampleMessage*.</span><span class="sxs-lookup"><span data-stu-id="87e28-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="87e28-177">Establecimiento y recuperación de un objeto completo en una variable</span><span class="sxs-lookup"><span data-stu-id="87e28-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="87e28-178">El código de ejemplo siguiente muestra cómo actualizar una variable con un valor complejo en un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="87e28-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="87e28-179">En este ejemplo, se recupera una máquina virtual de Azure con **Get-AzureVM** y se guarda en una variable de Automatización existente.</span><span class="sxs-lookup"><span data-stu-id="87e28-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="87e28-180">Como se explica en [Tipos de variables](#variable-types), se almacena como un PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="87e28-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="87e28-181">En el código siguiente, el valor se recupera de la variable y se usa para iniciar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="87e28-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="87e28-182">Establecimiento y recuperación de una colección en una variable</span><span class="sxs-lookup"><span data-stu-id="87e28-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="87e28-183">El código de ejemplo siguiente muestra cómo usar una variable con un colección de valores complejos en un runbook textual.</span><span class="sxs-lookup"><span data-stu-id="87e28-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="87e28-184">En este ejemplo, se recuperan varias máquinas virtuales de Azure con **Get-AzureVM** y se guardan en una variable de Automatización existente.</span><span class="sxs-lookup"><span data-stu-id="87e28-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="87e28-185">Como se explica en [Tipos de variables](#variable-types), se almacena como una colección de objetos PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="87e28-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="87e28-186">En el código siguiente, la colección se recupera de la variable y se usa para iniciar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="87e28-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="87e28-187">Ejemplos de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="87e28-187">Graphical runbook samples</span></span>

<span data-ttu-id="87e28-188">En un runbook gráfico, agregue **Get-AutomationVariable** o **Set-AutomationVariable** haciendo clic con el botón derecho en la variable en el panel Biblioteca del editor gráfico y seleccionando la actividad que desee.</span><span class="sxs-lookup"><span data-stu-id="87e28-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Adición de una variable al lienzo](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="87e28-190">Configuración de valores de una variable</span><span class="sxs-lookup"><span data-stu-id="87e28-190">Setting values in a variable</span></span>
<span data-ttu-id="87e28-191">La imagen siguiente muestra las actividades de ejemplo para actualizar una variable con un valor simple en un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="87e28-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="87e28-192">En este ejemplo, se recupera una única máquina virtual de Azure con **Get-AzureRmVM** y se guarda el nombre del equipo en una variable de Automation existente con un tipo de cadena.</span><span class="sxs-lookup"><span data-stu-id="87e28-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="87e28-193">No importa si el [vínculo es una canalización o una secuencia](automation-graphical-authoring-intro.md#links-and-workflow) , puesto que solo esperamos un único objeto en la salida.</span><span class="sxs-lookup"><span data-stu-id="87e28-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![Establecimiento de una variable simple](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="87e28-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87e28-195">Next Steps</span></span>

* <span data-ttu-id="87e28-196">Para obtener más información sobre cómo conectar actividades en la creación gráfica, consulte [Vínculos y flujo de trabajo en Creación gráfica en Automatización de Azure](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="87e28-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="87e28-197">Para empezar a trabajar con cuadernos gráficos, consulte [Mi primer runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="87e28-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

