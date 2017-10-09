---
title: "recursos de automatización aaaAzure en soluciones de OMS | Documentos de Microsoft"
description: "Soluciones de OMS incluirá, normalmente runbooks en automatización de Azure tooautomate procesos como recopilar y procesar datos de supervisión.  Este artículo se describe cómo tooinclude runbooks y sus recursos relacionados en una solución."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="0ad99-104">Agregar la solución de administración de automatización de Azure recursos tooan OMS (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="0ad99-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="0ad99-105">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="0ad99-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="0ad99-106">Cualquier esquema que se describe a continuación es toochange de asunto.</span><span class="sxs-lookup"><span data-stu-id="0ad99-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="0ad99-107">[Soluciones de administración de OMS](operations-management-suite-solutions.md) incluirá, normalmente runbooks en automatización de Azure tooautomate procesos como recopilar y procesar datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="0ad99-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="0ad99-108">Además toorunbooks, cuentas de automatización incluye activos como variables y las programaciones que admiten runbooks hello usa en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="0ad99-109">Este artículo se describe cómo tooinclude runbooks y sus recursos relacionados en una solución.</span><span class="sxs-lookup"><span data-stu-id="0ad99-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="0ad99-110">Hello ejemplos en este artículo usan parámetros y variables que están bien soluciones toomanagement necesarias o habituales y se describen en [crear soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="0ad99-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="0ad99-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ad99-111">Prerequisites</span></span>
<span data-ttu-id="0ad99-112">En este artículo se da por supuesto que ya está familiarizado con hello siguiente información.</span><span class="sxs-lookup"><span data-stu-id="0ad99-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="0ad99-113">Cómo demasiado[crear una solución de administración](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="0ad99-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="0ad99-114">Hola la estructura de un [archivo de solución](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="0ad99-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="0ad99-115">Cómo demasiado[crear plantillas de administrador de recursos](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="0ad99-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="0ad99-116">Cuenta de Automation</span><span class="sxs-lookup"><span data-stu-id="0ad99-116">Automation account</span></span>
<span data-ttu-id="0ad99-117">Todos los recursos de Azure Automation están incluidos en una [cuenta de Automation](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="0ad99-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="0ad99-118">Como se describe en [OMS área de trabajo y la cuenta de automatización](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Hola cuenta de automatización no se incluye en la solución de administración de hello, pero debe existir antes de instala la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="0ad99-119">Si no está disponible, se producirá un error en la instalación de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="0ad99-120">nombre de Hola de cada recurso de automatización incluye Hola de su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="0ad99-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="0ad99-121">Esto se hace en soluciones de hello con hello **accountName** parámetro como en el siguiente ejemplo de un recurso de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="0ad99-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="0ad99-122">Runbooks</span></span>
<span data-ttu-id="0ad99-123">Debe incluir los runbooks utilizados por solución de hello en el archivo de solución de Hola para que se crean cuando se instala la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="0ad99-124">No puede contener cuerpo Hola de runbook de hello en la plantilla de hello aunque, por lo que debe publicar Hola runbook tooa ubicación pública a la que puede obtenerse por cualquier usuario que instala la solución.</span><span class="sxs-lookup"><span data-stu-id="0ad99-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="0ad99-125">[Runbook de automatización de Azure](../automation/automation-runbook-types.md) recursos tienen un tipo de **Microsoft.Automation/automationAccounts/runbooks** y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="0ad99-126">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="0ad99-127">propiedades de Hola de runbooks se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ad99-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-128">Property</span></span> | <span data-ttu-id="0ad99-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ad99-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="0ad99-130">runbookType</span></span> |<span data-ttu-id="0ad99-131">Especifica los tipos de Hola de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="0ad99-132">Script: script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ad99-132">Script - PowerShell script</span></span> <br><span data-ttu-id="0ad99-133">PowerShell: flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ad99-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="0ad99-134">GraphPowerShell: runbook de script de PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="0ad99-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="0ad99-135">GraphPowerShellWorkflow: runbook de flujo de trabajo de PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="0ad99-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="0ad99-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="0ad99-136">logProgress</span></span> |<span data-ttu-id="0ad99-137">Especifica si [registros de progreso](../automation/automation-runbook-output-and-messages.md) para hello runbook debe generarse.</span><span class="sxs-lookup"><span data-stu-id="0ad99-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="0ad99-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="0ad99-138">logVerbose</span></span> |<span data-ttu-id="0ad99-139">Especifica si [registros detallados](../automation/automation-runbook-output-and-messages.md) para hello runbook debe generarse.</span><span class="sxs-lookup"><span data-stu-id="0ad99-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="0ad99-140">description</span><span class="sxs-lookup"><span data-stu-id="0ad99-140">description</span></span> |<span data-ttu-id="0ad99-141">Descripción opcional para el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="0ad99-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="0ad99-142">publishContentLink</span></span> |<span data-ttu-id="0ad99-143">Especifica el contenido de Hola de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="0ad99-144">URI - Uri toohello contenido de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="0ad99-145">Será un archivo. ps1 para los runbooks de PowerShell y script, y un archivo de runbook gráfico exportado para un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="0ad99-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="0ad99-146">versión: versión de runbook de Hola para su propio seguimiento.</span><span class="sxs-lookup"><span data-stu-id="0ad99-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="0ad99-147">Trabajos de automatización</span><span class="sxs-lookup"><span data-stu-id="0ad99-147">Automation jobs</span></span>
<span data-ttu-id="0ad99-148">Cuando se inicia un runbook en Azure Automation, se crea un trabajo de automatización.</span><span class="sxs-lookup"><span data-stu-id="0ad99-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="0ad99-149">Puede agregar un inicio de tooautomatically la automatización de la tarea recursos tooyour solución un runbook cuando se instala la solución de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="0ad99-150">Este método es toostart normalmente se usan runbooks que se usan para la configuración inicial de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="0ad99-151">crear un runbook a intervalos regulares, toostart una [programación](#schedules) y un [la programación del trabajo](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="0ad99-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="0ad99-152">Recursos de trabajo tienen un tipo de **Microsoft.Automation/automationAccounts/jobs** y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="0ad99-153">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="0ad99-154">propiedades de Hola para trabajos de automatización se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ad99-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-155">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-155">Property</span></span> | <span data-ttu-id="0ad99-156">Description</span><span class="sxs-lookup"><span data-stu-id="0ad99-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-157">runbook</span><span class="sxs-lookup"><span data-stu-id="0ad99-157">runbook</span></span> |<span data-ttu-id="0ad99-158">Entidad de nombre único con el nombre de Hola de hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="0ad99-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="0ad99-159">parameters</span><span class="sxs-lookup"><span data-stu-id="0ad99-159">parameters</span></span> |<span data-ttu-id="0ad99-160">Entidad de cada valor de parámetro requerido por runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="0ad99-161">trabajo de Hello incluye el nombre de runbook de Hola y cualquier toobe de valores de parámetro enviado toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="0ad99-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="0ad99-162">trabajo de Hello debe [dependen](operations-management-suite-solutions-solution-file.md#resources) Hola runbook que se está iniciando desde runbook Hola debe crearse antes de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="0ad99-163">Si tiene varios runbooks que deben iniciarse, puede definir su orden teniendo un trabajo dependiente de cualquier otro trabajo que deba ejecutarse primero.</span><span class="sxs-lookup"><span data-stu-id="0ad99-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="0ad99-164">nombre de Hola de un recurso de trabajo debe contener un GUID que se asigna normalmente por un parámetro.</span><span class="sxs-lookup"><span data-stu-id="0ad99-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="0ad99-165">Puede obtener más información sobre los parámetros GUID en [Creating solutions in Operations Management Suite (OMS) (Creación de soluciones en Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="0ad99-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="0ad99-166">Certificados</span><span class="sxs-lookup"><span data-stu-id="0ad99-166">Certificates</span></span>
<span data-ttu-id="0ad99-167">[Certificados de automatización de Azure](../automation/automation-certificates.md) tienen un tipo de **Microsoft.Automation/automationAccounts/certificates** y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="0ad99-168">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="0ad99-169">propiedades de Hola de recursos de certificados se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ad99-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-170">Property</span></span> | <span data-ttu-id="0ad99-171">Description</span><span class="sxs-lookup"><span data-stu-id="0ad99-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="0ad99-172">base64Value</span></span> |<span data-ttu-id="0ad99-173">Valor de base 64 para el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="0ad99-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="0ad99-174">thumbprint</span></span> |<span data-ttu-id="0ad99-175">Huella digital de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="0ad99-176">Credenciales</span><span class="sxs-lookup"><span data-stu-id="0ad99-176">Credentials</span></span>
<span data-ttu-id="0ad99-177">[Credenciales de automatización de Azure](../automation/automation-credentials.md) tienen un tipo de **Microsoft.Automation/automationAccounts/credentials** y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="0ad99-178">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="0ad99-179">propiedades de Hola de recursos de la credencial se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ad99-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-180">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-180">Property</span></span> | <span data-ttu-id="0ad99-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ad99-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-182">userName</span><span class="sxs-lookup"><span data-stu-id="0ad99-182">userName</span></span> |<span data-ttu-id="0ad99-183">Nombre de usuario para las credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-183">User name for hello credential.</span></span> |
| <span data-ttu-id="0ad99-184">Contraseña</span><span class="sxs-lookup"><span data-stu-id="0ad99-184">password</span></span> |<span data-ttu-id="0ad99-185">Contraseña de la credencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="0ad99-186">Programaciones</span><span class="sxs-lookup"><span data-stu-id="0ad99-186">Schedules</span></span>
<span data-ttu-id="0ad99-187">[Programaciones de automatización de Azure](../automation/automation-schedules.md) tienen un tipo de **Microsoft.Automation/automationAccounts/schedules** y tener Hola Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="0ad99-188">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="0ad99-189">propiedades de Hola para programar los recursos se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ad99-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-190">Property</span></span> | <span data-ttu-id="0ad99-191">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ad99-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-192">description</span><span class="sxs-lookup"><span data-stu-id="0ad99-192">description</span></span> |<span data-ttu-id="0ad99-193">Descripción opcional para la programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="0ad99-194">startTime</span><span class="sxs-lookup"><span data-stu-id="0ad99-194">startTime</span></span> |<span data-ttu-id="0ad99-195">Especifica la hora de inicio de Hola de una programación como un objeto DateTime.</span><span class="sxs-lookup"><span data-stu-id="0ad99-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="0ad99-196">Puede proporcionar una cadena si se puede convertir tooa DateTime válido.</span><span class="sxs-lookup"><span data-stu-id="0ad99-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="0ad99-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="0ad99-197">isEnabled</span></span> |<span data-ttu-id="0ad99-198">Especifica si está habilitada la programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="0ad99-199">interval</span><span class="sxs-lookup"><span data-stu-id="0ad99-199">interval</span></span> |<span data-ttu-id="0ad99-200">tipo de Hola de intervalo de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="0ad99-201">day</span><span class="sxs-lookup"><span data-stu-id="0ad99-201">day</span></span><br><span data-ttu-id="0ad99-202">hour</span><span class="sxs-lookup"><span data-stu-id="0ad99-202">hour</span></span> |
| <span data-ttu-id="0ad99-203">frequency</span><span class="sxs-lookup"><span data-stu-id="0ad99-203">frequency</span></span> |<span data-ttu-id="0ad99-204">Frecuencia con la que Hola programación debería desencadenar en número de días u horas.</span><span class="sxs-lookup"><span data-stu-id="0ad99-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="0ad99-205">Programa debe tener una hora de inicio con un valor mayor que Hola hora actual.</span><span class="sxs-lookup"><span data-stu-id="0ad99-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="0ad99-206">No puede proporcionar este valor con una variable, ya que no tendría ninguna manera de saber si se trata de toobe va instalado.</span><span class="sxs-lookup"><span data-stu-id="0ad99-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="0ad99-207">Utilice uno de hello siguiendo dos estrategias al usar recursos de programación en una solución.</span><span class="sxs-lookup"><span data-stu-id="0ad99-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="0ad99-208">Usar un parámetro de hora de inicio de Hola de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="0ad99-209">Al instalar soluciones de hello, se le pedirá Hola usuario tooprovide un valor.</span><span class="sxs-lookup"><span data-stu-id="0ad99-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="0ad99-210">Si tiene varias programaciones, podría usar un valor del parámetro único para más de una.</span><span class="sxs-lookup"><span data-stu-id="0ad99-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="0ad99-211">Crear programaciones de hello utilizando un runbook que se inicia cuando se instala la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="0ad99-212">Esto elimina la necesidad de Hola de hello toospecify de usuario una vez, pero no puede contener programación hello en la solución, por lo que se quitarán cuando se quita la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="0ad99-213">Programaciones del trabajo</span><span class="sxs-lookup"><span data-stu-id="0ad99-213">Job schedules</span></span>
<span data-ttu-id="0ad99-214">Los recursos de programación de trabajo vinculan un runbook con una programación.</span><span class="sxs-lookup"><span data-stu-id="0ad99-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="0ad99-215">Tienen un tipo de **Microsoft.Automation/automationAccounts/jobSchedules** y tener Hola Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="0ad99-216">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="0ad99-217">en hello en la tabla siguiente se describen propiedades de Hola para las programaciones de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0ad99-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-218">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-218">Property</span></span> | <span data-ttu-id="0ad99-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ad99-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-220">nombre de programación</span><span class="sxs-lookup"><span data-stu-id="0ad99-220">schedule name</span></span> |<span data-ttu-id="0ad99-221">Solo **nombre** entidad con el nombre de Hola de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="0ad99-222">nombre de runbook</span><span class="sxs-lookup"><span data-stu-id="0ad99-222">runbook name</span></span>  |<span data-ttu-id="0ad99-223">Solo **nombre** entidad con el nombre de Hola de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="0ad99-224">variables</span><span class="sxs-lookup"><span data-stu-id="0ad99-224">Variables</span></span>
<span data-ttu-id="0ad99-225">[Variables de automatización de Azure](../automation/automation-variables.md) tienen un tipo de **Microsoft.Automation/automationAccounts/variables** y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="0ad99-226">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="0ad99-227">propiedades de Hola de variable recursos se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ad99-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-228">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-228">Property</span></span> | <span data-ttu-id="0ad99-229">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ad99-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-230">description</span><span class="sxs-lookup"><span data-stu-id="0ad99-230">description</span></span> | <span data-ttu-id="0ad99-231">Descripción opcional para la variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="0ad99-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="0ad99-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="0ad99-232">isEncrypted</span></span> | <span data-ttu-id="0ad99-233">Especifica si se debe cifrar la variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="0ad99-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="0ad99-234">type</span><span class="sxs-lookup"><span data-stu-id="0ad99-234">type</span></span> | <span data-ttu-id="0ad99-235">Esta propiedad no tiene actualmente ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="0ad99-235">This property currently has no effect.</span></span>  <span data-ttu-id="0ad99-236">tipo de datos de Hola de variable de saludo se determinará por el valor inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="0ad99-237">value</span><span class="sxs-lookup"><span data-stu-id="0ad99-237">value</span></span> | <span data-ttu-id="0ad99-238">Valor de variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="0ad99-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="0ad99-239">Hola **tipo** propiedad no tiene ningún efecto en la variable de saludo que se está creando.</span><span class="sxs-lookup"><span data-stu-id="0ad99-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="0ad99-240">Hola de tipo de datos para la variable de saludo se determinará por el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="0ad99-241">Si establece el valor inicial de hello para la variable de hello, debe configurarse como tipo de datos correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="0ad99-242">Hello en la tabla siguiente proporciona Hola distintos tipos de datos permitidos y su sintaxis.</span><span class="sxs-lookup"><span data-stu-id="0ad99-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="0ad99-243">Tenga en cuenta que los valores de JSON sean tooalways esperado ir entre comillas con los caracteres especiales dentro de las comillas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="0ad99-244">Por ejemplo, un valor de cadena se especificarían por comillas alrededor de la cadena de hello (utilizando el carácter de escape de hello (\\)) mientras se especifica un valor numérico con un conjunto de comillas.</span><span class="sxs-lookup"><span data-stu-id="0ad99-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="0ad99-245">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="0ad99-245">Data type</span></span> | <span data-ttu-id="0ad99-246">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ad99-246">Description</span></span> | <span data-ttu-id="0ad99-247">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0ad99-247">Example</span></span> | <span data-ttu-id="0ad99-248">Resuelve demasiado</span><span class="sxs-lookup"><span data-stu-id="0ad99-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="0ad99-249">cadena</span><span class="sxs-lookup"><span data-stu-id="0ad99-249">string</span></span>   | <span data-ttu-id="0ad99-250">Incluya el valor entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="0ad99-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="0ad99-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="0ad99-251">"\"Hello world\""</span></span> | <span data-ttu-id="0ad99-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="0ad99-252">"Hello world"</span></span> |
| <span data-ttu-id="0ad99-253">numeric</span><span class="sxs-lookup"><span data-stu-id="0ad99-253">numeric</span></span>  | <span data-ttu-id="0ad99-254">Valor numérico con comillas simples.</span><span class="sxs-lookup"><span data-stu-id="0ad99-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="0ad99-255">"64"</span><span class="sxs-lookup"><span data-stu-id="0ad99-255">"64"</span></span> | <span data-ttu-id="0ad99-256">64</span><span class="sxs-lookup"><span data-stu-id="0ad99-256">64</span></span> |
| <span data-ttu-id="0ad99-257">boolean</span><span class="sxs-lookup"><span data-stu-id="0ad99-257">boolean</span></span>  | <span data-ttu-id="0ad99-258">**true** o **false** entre comillas.</span><span class="sxs-lookup"><span data-stu-id="0ad99-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="0ad99-259">Tenga en cuenta que este valor debe ir en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0ad99-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="0ad99-260">"true"</span><span class="sxs-lookup"><span data-stu-id="0ad99-260">"true"</span></span> | <span data-ttu-id="0ad99-261">true</span><span class="sxs-lookup"><span data-stu-id="0ad99-261">true</span></span> |
| <span data-ttu-id="0ad99-262">datetime</span><span class="sxs-lookup"><span data-stu-id="0ad99-262">datetime</span></span> | <span data-ttu-id="0ad99-263">Valor de fecha serializado.</span><span class="sxs-lookup"><span data-stu-id="0ad99-263">Serialized date value.</span></span><br><span data-ttu-id="0ad99-264">Puede usar este valor de cmdlet ConvertTo-Json de hello en toogenerate de PowerShell para una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="0ad99-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="0ad99-265">Ejemplo: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="0ad99-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="0ad99-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="0ad99-266">ConvertTo-Json</span></span> | <span data-ttu-id="0ad99-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="0ad99-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="0ad99-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="0ad99-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="0ad99-269">Módulos</span><span class="sxs-lookup"><span data-stu-id="0ad99-269">Modules</span></span>
<span data-ttu-id="0ad99-270">La solución de administración no es necesario toodefine [módulos globales](../automation/automation-integration-modules.md) utilizada por los runbooks ya que siempre estén disponibles en su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="0ad99-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="0ad99-271">Es necesario tooinclude un recurso para cualquier otro módulo utilizado por los runbooks.</span><span class="sxs-lookup"><span data-stu-id="0ad99-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="0ad99-272">[Módulos de integración](../automation/automation-integration-modules.md) tienen un tipo de **Microsoft.Automation/automationAccounts/modules** y tener Hola siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="0ad99-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="0ad99-273">Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="0ad99-274">propiedades de Hola de recursos de módulo se describen en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ad99-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="0ad99-275">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0ad99-275">Property</span></span> | <span data-ttu-id="0ad99-276">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ad99-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ad99-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="0ad99-277">contentLink</span></span> |<span data-ttu-id="0ad99-278">Especifica el contenido de hello del módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="0ad99-279">URI - Uri toohello contenido del módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="0ad99-280">Será un archivo. ps1 para los runbooks de PowerShell y script, y un archivo de runbook gráfico exportado para un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="0ad99-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="0ad99-281">versión: versión del módulo de Hola para su propio seguimiento.</span><span class="sxs-lookup"><span data-stu-id="0ad99-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="0ad99-282">Hola runbook debe depender de hello módulo recursos tooensure que ha creado antes de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="0ad99-283">Actualización de módulos</span><span class="sxs-lookup"><span data-stu-id="0ad99-283">Updating modules</span></span>
<span data-ttu-id="0ad99-284">Si actualiza una solución de administración que incluya un runbook que utiliza una programación y Hola nueva versión de la solución tiene un nuevo módulo por ese runbook, Hola runbook puede usar versión anterior de hello del módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="0ad99-285">Debe incluir Hola después runbooks en la solución y crear un trabajo toorun automáticamente antes de los otros runbooks.</span><span class="sxs-lookup"><span data-stu-id="0ad99-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="0ad99-286">Esto garantizará que los módulos que se actualizan como Hola necesario antes de cargar los runbooks.</span><span class="sxs-lookup"><span data-stu-id="0ad99-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="0ad99-287">[Actualización ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) se asegurará de que todos los módulos de hello usan los runbooks en la solución de son la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="0ad99-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) se vuelva a registrar todas tooensure de recursos de programación Hola que Hola runbooks vinculados toothem con módulos de uso hello más recientes.</span><span class="sxs-lookup"><span data-stu-id="0ad99-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="0ad99-289">Muestra</span><span class="sxs-lookup"><span data-stu-id="0ad99-289">Sample</span></span>
<span data-ttu-id="0ad99-290">Aquí te mostramos un ejemplo de una solución que incluya incluye Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0ad99-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="0ad99-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="0ad99-291">Runbook.</span></span>  <span data-ttu-id="0ad99-292">Este es un runbook de ejemplo almacenado en un repositorio de GitHub público.</span><span class="sxs-lookup"><span data-stu-id="0ad99-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="0ad99-293">Trabajo de automatización que se inicia Hola runbook cuando se instala la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="0ad99-294">Programación y trabajo programación toostart Hola runbook a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="0ad99-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="0ad99-295">Certificado.</span><span class="sxs-lookup"><span data-stu-id="0ad99-295">Certificate.</span></span>
- <span data-ttu-id="0ad99-296">Credencial.</span><span class="sxs-lookup"><span data-stu-id="0ad99-296">Credential.</span></span>
- <span data-ttu-id="0ad99-297">Variable.</span><span class="sxs-lookup"><span data-stu-id="0ad99-297">Variable.</span></span>
- <span data-ttu-id="0ad99-298">Módulo.</span><span class="sxs-lookup"><span data-stu-id="0ad99-298">Module.</span></span>  <span data-ttu-id="0ad99-299">Se trata de hello [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) para escribir datos tooLog análisis.</span><span class="sxs-lookup"><span data-stu-id="0ad99-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="0ad99-300">usos de ejemplo de Hola [parámetros de la solución estándar](operations-management-suite-solutions-solution-file.md#parameters) variables que normalmente se utilizarían en una solución como opone toohardcoding valores en las definiciones de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ad99-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="0ad99-301">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ad99-301">Next steps</span></span>
* <span data-ttu-id="0ad99-302">[Agregar una solución de tooyour vista](operations-management-suite-solutions-resources-views.md) toovisualize los datos recopilados.</span><span class="sxs-lookup"><span data-stu-id="0ad99-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
