---
title: "<span data-ttu-id=\"beea1-101\">Creación de módulos de integración de Azure Automation | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"beea1-101\">Create an Azure Automation Integration Module | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"beea1-102\">En este tutorial se explica cómo crear y probar módulos de integración en Azure Automation y se proporcionan ejemplos de uso.</span><span class=\"sxs-lookup\"><span data-stu-id=\"beea1-102\">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="beea1-103">Módulos de integración de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="beea1-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="beea1-104">PowerShell es la principal tecnología que se esconde detrás de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="beea1-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="beea1-105">Desde que Automatización de Azure se integró en PowerShell, los módulos de PowerShell resultan clave para la extensibilidad de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="beea1-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="beea1-106">En este artículo, explicaremos los aspectos específicos sobre el uso de los módulos de PowerShell en Automatización de Azure, lo que se conoce como “Módulos de integración”, y los procedimientos recomendados para que pueda crear sus propios módulos de PowerShell y asegurarse de que funcionan como módulos de integración en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="beea1-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="beea1-107">¿Qué son los módulos de PowerShell?</span><span class="sxs-lookup"><span data-stu-id="beea1-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="beea1-108">Un módulo de PowerShell es un grupo de cmdlets de PowerShell, como **Get-Date** o **Copy-Item**, que se puede usar en la consola, los scripts, los flujos de trabajo y los Runbooks de PowerShell, y un grupo de recursos de DSC de PowerShell, como WindowsFeature o File, que se puede utilizar en las configuraciones de DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beea1-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="beea1-109">Toda la funcionalidad de PowerShell se expone a través de cmdlets y recursos de DSC. Todos los cmdlets y recursos de DSC se guardan en una copia de seguridad en un módulo de PowerShell, y muchos de los ellos se envían al propio PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beea1-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="beea1-110">Por ejemplo, el cmdlet **Get-Date** forma parte del módulo Microsoft.PowerShell.Utility de PowerShell, el cmdlet **Copy-Item** forma parte del módulo Microsoft.PowerShell.Management de PowerShell y el recurso Package de DSC forma parte del módulo PSDesiredStateConfiguration de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beea1-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="beea1-111">Estos módulos se suministran con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beea1-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="beea1-112">Sin embargo, muchos otros módulos no están incluidos en PowerShell y se distribuyen a través de productos propios o de terceros, como System Center 2012 Configuration Manager, o a través de los lugares que conforman la vasta comunidad de PowerShell, como la Galería de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beea1-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="beea1-113">Los módulos resultan muy útiles, ya que simplifican las tareas complejas gracias a su funcionalidad encapsulada.</span><span class="sxs-lookup"><span data-stu-id="beea1-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="beea1-114">Puede obtener más información sobre los [módulos de PowerShell en MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="beea1-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="beea1-115">¿Qué son los módulos de integración de Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="beea1-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="beea1-116">Los módulos de integración se parecen mucho a los módulos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beea1-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="beea1-117">Sencillamente, se trata de módulos de PowerShell que, de manera opcional, pueden contener un archivo adicional: un archivo de metadatos que especifica un tipo de conexión de Automatización de Azure que se va a utilizar con los cmdlets del módulo en los Runbooks.</span><span class="sxs-lookup"><span data-stu-id="beea1-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="beea1-118">Tanto si incluyen como si no el archivo opcional, estos módulos de PowerShell pueden importarse en Automatización de Azure para que sus cmdlets estén disponibles y puedan usarse en Runbooks y para que sus recursos de DSC estén disponibles y puedan usarse en las configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="beea1-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="beea1-119">En segundo plano, Azure Automation almacena estos módulos en segundo plano y en el tiempo de ejecución del trabajo de compilación de DSC y del trabajo de runbook, los carga en espacios aislados de Azure Automation, donde se ejecutan los runbooks y se compilan las configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="beea1-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="beea1-120">Todos los recursos de DSC de los módulos se sitúan automáticamente en el servidor de extracción de DSC de Automatización para que las máquinas que intentan aplicar las configuraciones de DSC puedan extraerlos.</span><span class="sxs-lookup"><span data-stu-id="beea1-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="beea1-121">De forma estándar, Azure Automation contiene varios módulos de Azure PowerShell que se pueden usar para empezar a automatizar directamente la administración de Azure. No obstante, también puede importar módulos de PowerShell para cualquier sistema, servicio o herramienta con los que quiera integrarlos.</span><span class="sxs-lookup"><span data-stu-id="beea1-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="beea1-122">Algunos módulos se suministran como "módulos globales" en el servicio de Automatización.</span><span class="sxs-lookup"><span data-stu-id="beea1-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="beea1-123">Estos módulos globales están disponibles cuando se crea una cuenta de Automatización y los actualizamos a veces, lo que los expulsa automáticamente de su cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="beea1-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="beea1-124">Si no desea que se actualicen automáticamente, siempre puede importar el mismo módulo, y que tendrá prioridad sobre la versión del módulo global de dicho módulo que se incluye en el servicio.</span><span class="sxs-lookup"><span data-stu-id="beea1-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="beea1-125">El formato para importar un paquete de módulo de integración es un archivo comprimido que tiene el mismo nombre del módulo y una extensión .zip.</span><span class="sxs-lookup"><span data-stu-id="beea1-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="beea1-126">El paquete contiene el módulo de Windows PowerShell y todos los archivos auxiliares, como el archivo de manifiesto (.psd1), si es que el módulo tiene uno.</span><span class="sxs-lookup"><span data-stu-id="beea1-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="beea1-127">Si el módulo debe contener un tipo de conexión de Azure Automation, también debe incluir un archivo llamado `<ModuleName>-Automation.json` que especifique las propiedades del tipo de conexión.</span><span class="sxs-lookup"><span data-stu-id="beea1-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="beea1-128">Este archivo json se encuentra dentro de la carpeta del módulo del archivo .zip y contiene los campos de una “conexión” que es necesaria para poder conectarse al sistema o servicio que el módulo representa.</span><span class="sxs-lookup"><span data-stu-id="beea1-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="beea1-129">De este modo, se creará un tipo de conexión en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="beea1-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="beea1-130">Con este archivo, puede configurar los nombres y los tipos de campo del tipo de conexión del módulo, además de especificar si los campos deben cifrarse o el cifrado es opcional.</span><span class="sxs-lookup"><span data-stu-id="beea1-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="beea1-131">A continuación, se incluye una plantilla con el formato del archivo json:</span><span class="sxs-lookup"><span data-stu-id="beea1-131">The following is a template in the json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="beea1-132">Si ha implementado Service Management Automation y ha creado paquetes de módulos de integración para los Runbooks de Automatización, esta plantilla le resultará familiar.</span><span class="sxs-lookup"><span data-stu-id="beea1-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="beea1-133">Procedimientos recomendados sobre la creación de los módulos</span><span class="sxs-lookup"><span data-stu-id="beea1-133">Authoring Best Practices</span></span>
<span data-ttu-id="beea1-134">Aunque los módulos de integración son esencialmente módulos de Powershell, hay una serie de recomendaciones que debe tener en cuenta al crear módulos de PowerShell para facilitar su uso en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="beea1-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="beea1-135">Algunas de estas recomendaciones son específicas de Automatización de Azure, mientras que otras resultan útiles para que los módulos funcionen bien en el flujo de trabajo de PowerShell, con independencia de si se usa o no Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="beea1-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="beea1-136">Incluya una sinopsis, una descripción y un identificador URI de ayuda para todos los cmdlets del módulo.</span><span class="sxs-lookup"><span data-stu-id="beea1-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="beea1-137">En PowerShell, puede definir cierta información de ayuda para los cmdlets de forma que al usuario le resulte más fácil usarlos con el cmdlet **Get-Help** .</span><span class="sxs-lookup"><span data-stu-id="beea1-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="beea1-138">Por ejemplo, a continuación le mostramos cómo puede definir una sinopsis y un identificador URI de ayuda para un módulo de PowerShell escrito en un archivo .psm1.</span><span class="sxs-lookup"><span data-stu-id="beea1-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="beea1-139">Esta información no solo sirve para proporcionar ayuda cuando se usa el cmdlet **Get-Help** en la consola de PowerShell, sino que también expondrá esta funcionalidad de ayuda en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="beea1-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="beea1-140">Por ejemplo, al insertar actividades durante la creación de runbooks.</span><span class="sxs-lookup"><span data-stu-id="beea1-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="beea1-141">Al hacer clic en “Ver ayuda detallada”, el identificador URI de ayuda se abrirá en otra pestaña del explorador web que esté utilizando para acceder a Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="beea1-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="beea1-142">![Ayuda para los módulos de integración](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="beea1-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="beea1-143">Si el módulo se ejecuta en un sistema remoto,</span><span class="sxs-lookup"><span data-stu-id="beea1-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="beea1-144">a.</span><span class="sxs-lookup"><span data-stu-id="beea1-144">a.</span></span> <span data-ttu-id="beea1-145">debería incluir un archivo de metadatos del módulo de integración que defina la información necesaria para conectarse a ese sistema remoto (es decir, el tipo de conexión).</span><span class="sxs-lookup"><span data-stu-id="beea1-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="beea1-146">b.</span><span class="sxs-lookup"><span data-stu-id="beea1-146">b.</span></span> <span data-ttu-id="beea1-147">En segundo lugar, cada cmdlet del módulo debería poder tomar como parámetro un objeto de conexión (una instancia del tipo de conexión).</span><span class="sxs-lookup"><span data-stu-id="beea1-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="beea1-148">Los cmdlets del módulo resultan más fáciles de usar en Automatización de Azure si permite que se les pase como parámetro un objeto con los campos del tipo de conexión.</span><span class="sxs-lookup"><span data-stu-id="beea1-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="beea1-149">De este modo, cada vez que los usuarios invoquen un cmdlet, no tendrán que asignar parámetros del recurso de conexión a los parámetros correspondientes del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="beea1-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="beea1-150">En el ejemplo de Runbook anterior, se utiliza un recurso de conexión Twilio denominado «CorpTwilio» para acceder a Twilio y devolver todos los números de teléfono de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="beea1-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="beea1-151">Observe cómo se asignan los campos de la conexión a los parámetros del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="beea1-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="beea1-152">Existe otra forma más fácil y eficaz de hacer esto, y consiste en pasar directamente el objeto de conexión al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="beea1-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="beea1-153">Para habilitar un comportamiento como este en sus cmdlets, permítales que acepten directamente un objeto de conexión como parámetro en lugar de usar solamente campos de conexión en los parámetros.</span><span class="sxs-lookup"><span data-stu-id="beea1-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="beea1-154">Normalmente, necesitará un conjunto de parámetros para cada uno de ellos, de forma que los usuarios que no utilicen Automatización de Azure puedan llamar a los cmdlets sin necesidad de crear una tabla hash que actúe como objeto de conexión.</span><span class="sxs-lookup"><span data-stu-id="beea1-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="beea1-155">En el fragmento de código siguiente, el conjunto de parámetros **SpecifyConnectionFields** se utiliza para pasar las propiedades de los campos de conexión de una en una.</span><span class="sxs-lookup"><span data-stu-id="beea1-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="beea1-156">**UseConnectionObject** permite pasar directamente la conexión.</span><span class="sxs-lookup"><span data-stu-id="beea1-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="beea1-157">Como puede ver, el cmdlet Send-TwilioSMS del [módulo de PowerShell de Twilio](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) permite utilizar cualquiera de estos mecanismos para pasar valores:</span><span class="sxs-lookup"><span data-stu-id="beea1-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="beea1-158">Defina el tipo de salida de todos los cmdlets del módulo.</span><span class="sxs-lookup"><span data-stu-id="beea1-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="beea1-159">Definir un tipo de salida en un cmdlet permite que IntelliSense le ayude a determinar, en tiempo de diseño, las propiedades de salida del cmdlet, lo que resultará útil durante la creación.</span><span class="sxs-lookup"><span data-stu-id="beea1-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="beea1-160">Esto resulta especialmente útil durante la creación gráfica de un Runbook de Automatización, donde la información en tiempo de diseño resulta esencial para facilitar la experiencia del usuario con el módulo.</span><span class="sxs-lookup"><span data-stu-id="beea1-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="beea1-161">![Tipo de salida de runbooks gráficos](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="beea1-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="beea1-162">Esto proporciona una funcionalidad similar a la funcionalidad "type ahead" de la salida de los cmdlets de PowerShell ISE sin necesidad de ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="beea1-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="beea1-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="beea1-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="beea1-164">Los cmdlets del módulo no deben tomar tipos de objetos complejos como parámetros.</span><span class="sxs-lookup"><span data-stu-id="beea1-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="beea1-165">El flujo de trabajo de PowerShell se diferencia del propio PowerShell en que almacena tipos complejos con formato deserializado.</span><span class="sxs-lookup"><span data-stu-id="beea1-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="beea1-166">Los tipos primitivos seguirán siendo primitivos. Sin embargo, los tipos complejos se convierten en sus versiones deserializadas, por lo que básicamente constituyen bolsas de propiedades.</span><span class="sxs-lookup"><span data-stu-id="beea1-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="beea1-167">Por ejemplo, si utiliza el cmdlet **Get-Process** en un Runbook (o, en este caso, en un flujo de trabajo de PowerShell), el cmdlet devolverá un objeto de tipo [Deserialized.System.Diagnostic.Process] en lugar del tipo esperado: [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="beea1-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="beea1-168">Este tipo tiene las mismas propiedades que el tipo no deserializado, pero no contiene ninguno de los métodos.</span><span class="sxs-lookup"><span data-stu-id="beea1-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="beea1-169">Además, si intenta pasar este valor como parámetro a un cmdlet (donde el cmdlet espera un valor [System.Diagnostic.Process] para este parámetro), aparecerá el siguiente error: *No se puede procesar la transformación del argumento del parámetro 'process'. Error: "No se puede convertir el valor "System.Diagnostics.Process (CcmExec)" de tipo "Deserialized.System.Diagnostics.Process" al tipo "System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="beea1-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="beea1-170">Esto se debe a que hay un error de concordancia de tipos entre el tipo esperado, [System.Diagnostic.Process], y el tipo proporcionado, [Deserialized.System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="beea1-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="beea1-171">El modo de solucionar este problema es garantizar que los cmdlets del módulo no toman tipos complejos como parámetros.</span><span class="sxs-lookup"><span data-stu-id="beea1-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="beea1-172">Este es el modo incorrecto de hacerlo.</span><span class="sxs-lookup"><span data-stu-id="beea1-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="beea1-173">Y este es el modo correcto, donde se toma un primitivo que el cmdlet puede usar internamente para captar el objeto complejo y utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="beea1-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="beea1-174">Como los cmdlets se ejecutan en el contexto de PowerShell, y no en el del flujo de trabajo de PowerShell, el cmdlet $process se transforma en el tipo adecuado, [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="beea1-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="beea1-175">Los recursos de conexión de los Runbooks son tablas hash, que son de tipo complejo. Sin embargo, parece que estas tablas hash pueden pasarse sin problemas a los cmdlets como parámetro –Connection, sin ninguna excepción de conversión.</span><span class="sxs-lookup"><span data-stu-id="beea1-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="beea1-176">Técnicamente, algunos tipos de PowerShell pueden convertirse correctamente de su formato serializado al formato deserializado y, por tanto, pueden pasarse a los cmdlets en los parámetros que aceptan tipos no deserializados.</span><span class="sxs-lookup"><span data-stu-id="beea1-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="beea1-177">Las tablas hash son uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="beea1-177">Hashtable is one of these.</span></span> <span data-ttu-id="beea1-178">Es posible que los tipos definidos por el creador de un módulo se implementen de forma que también puedan deserializarse correctamente, pero hay que tener en cuenta algunos equilibrios.</span><span class="sxs-lookup"><span data-stu-id="beea1-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="beea1-179">El tipo debe tener un constructor predeterminado, todas sus propiedades deben ser públicas y debe tener un objeto PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="beea1-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="beea1-180">Sin embargo, en los tipos que ya están definidos y que no son propiedad del creador del módulo, no hay forma de “corregirlos” y, por tanto, se recomienda evitar tipos complejos en todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="beea1-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="beea1-181">Sugerencia sobre la creación de Runbooks: si, por alguna razón, los cmdlets deben tomar un parámetro de tipo complejo o está utilizando el módulo de otra persona que requiere un parámetro de este tipo, la solución para los Runbooks del flujo de trabajo de PowerShell y los flujos de trabajo de instancias de PowerShell locales es encapsular el cmdlet que genera el tipo complejo y el cmdlet que lo consume en la misma actividad de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="beea1-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="beea1-182">Dado que InlineScript ejecuta su contenido como PowerShell y no como el flujo de trabajo de PowerShell, el cmdlet que genera el tipo complejo crearía el tipo correcto, y no el tipo complejo deserializado.</span><span class="sxs-lookup"><span data-stu-id="beea1-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="beea1-183">Cree todos los cmdlets del módulo sin estado.</span><span class="sxs-lookup"><span data-stu-id="beea1-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="beea1-184">El flujo de trabajo de PowerShell ejecuta cada uno de los cmdlets que se invocan durante el flujo de trabajo en una sesión diferente.</span><span class="sxs-lookup"><span data-stu-id="beea1-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="beea1-185">Esto significa que los cmdlets que dependan de un estado de sesión creado o modificado por otros cmdlets del mismo módulo no funcionarán en los Runbooks del flujo de trabajo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beea1-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="beea1-186">A continuación se muestra un ejemplo de lo que no hay que hacer:</span><span class="sxs-lookup"><span data-stu-id="beea1-186">Here is an example of what not to do.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="beea1-187">El módulo debe estar incluido en su totalidad en un paquete compatible con Xcopy.</span><span class="sxs-lookup"><span data-stu-id="beea1-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="beea1-188">Como los módulos de Automatización de Azure se distribuyen en espacios aislados de Automatización cuando es necesario ejecutar los Runbooks, no pueden depender del host en el que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="beea1-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="beea1-189">Esto significa que debería poder comprimir el paquete del módulo en un zip, trasladarlo a otro host que tenga la misma versión de PowerShell, u otra posterior, y conseguir que funcione normalmente cuando se importe en el entorno de PowerShell de dicho host.</span><span class="sxs-lookup"><span data-stu-id="beea1-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="beea1-190">Para que esto ocurra, el módulo no debe depender de ningún archivo que esté fuera de la carpeta del módulo (la carpeta que se comprime al importar en Automatización de Azure) ni de ninguna configuración única del Registro de un host, como las que se establecen al instalar un producto.</span><span class="sxs-lookup"><span data-stu-id="beea1-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="beea1-191">Si no se sigue este procedimiento recomendado, el módulo no podrá utilizarse en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="beea1-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="beea1-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="beea1-192">Next steps</span></span>

* <span data-ttu-id="beea1-193">Para empezar a trabajar con Runbooks de flujo de trabajo de PowerShell, consulte [Mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="beea1-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="beea1-194">Para más información sobre la creación de módulos de PowerShell, consulte [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="beea1-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

