---
title: Recursos de Azure Automation en soluciones de OMS | Microsoft Docs
description: "Normalmente, las soluciones de OMS incluyen runbooks en Azure Automation para automatizar procesos como la recopilación y el procesamiento de datos de supervisión.  En este artículo se describe cómo incluir runbooks y sus recursos relacionados en una solución."
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
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="08cb7-104">Incorporación de recursos de Azure Automation a una solución de administración de OMS (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="08cb7-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="08cb7-105">La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar.</span><span class="sxs-lookup"><span data-stu-id="08cb7-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="08cb7-106">Cualquier esquema descrito a continuación está sujeto a cambios.</span><span class="sxs-lookup"><span data-stu-id="08cb7-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="08cb7-107">[Normalmente, las soluciones de administración de OMS](operations-management-suite-solutions.md) incluyen runbooks en Azure Automation para automatizar procesos como la recopilación y el procesamiento de datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="08cb7-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="08cb7-108">Además de los runbooks, las cuentas de Automation incluyen recursos como variables y programaciones que admiten los runbooks que se usan en la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="08cb7-109">En este artículo se describe cómo incluir runbooks y sus recursos relacionados en una solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="08cb7-110">En los ejemplos de este artículo se usan parámetros y variables que son necesarios o comunes para las soluciones de administración y se describen en [Creating management solutions in Operations Management Suite (OMS) (Creación de soluciones de administración en Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="08cb7-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="08cb7-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="08cb7-111">Prerequisites</span></span>
<span data-ttu-id="08cb7-112">En este artículo se supone que ya está familiarizado con la información siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="08cb7-113">Cómo [crear una solución de administración](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="08cb7-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="08cb7-114">La estructura de un [archivo de solución](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="08cb7-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="08cb7-115">Cómo [crear plantillas de Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="08cb7-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="08cb7-116">Cuenta de Automation</span><span class="sxs-lookup"><span data-stu-id="08cb7-116">Automation account</span></span>
<span data-ttu-id="08cb7-117">Todos los recursos de Azure Automation están incluidos en una [cuenta de Automation](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="08cb7-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="08cb7-118">Como se describe en [el área de trabajo de OMS y la cuenta de Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account), la cuenta de Automation no está incluida en la solución de administración pero debe existir antes de que se instale la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="08cb7-119">Si no está disponible, se producirá un error en la instalación de la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="08cb7-120">El nombre de cada recurso de Automation incluye el nombre de su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="08cb7-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="08cb7-121">Esto se hace en la solución con el parámetro **accountName** como se muestra en el siguiente ejemplo de un recurso de runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="08cb7-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="08cb7-122">Runbooks</span></span>
<span data-ttu-id="08cb7-123">Debe incluir cualquier runbook usado por la solución en el archivo de solución de modo que se creen al instalarse la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="08cb7-124">No puede contener el cuerpo del runbook en la plantilla, sin embargo, por lo que debe publicar el runbook en una ubicación pública a la que pueda tener acceso cualquier usuario que instale su solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="08cb7-125">Los recursos de [runbook de Azure Automation](../automation/automation-runbook-types.md) tienen un tipo de **Microsoft.Automation/automationAccounts/runbooks** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="08cb7-126">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="08cb7-127">En la tabla siguiente se describen las propiedades para los runbooks.</span><span class="sxs-lookup"><span data-stu-id="08cb7-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="08cb7-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-128">Property</span></span> | <span data-ttu-id="08cb7-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="08cb7-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="08cb7-130">runbookType</span></span> |<span data-ttu-id="08cb7-131">Especifica los tipos del runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="08cb7-132">Script: script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="08cb7-132">Script - PowerShell script</span></span> <br><span data-ttu-id="08cb7-133">PowerShell: flujo de trabajo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="08cb7-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="08cb7-134">GraphPowerShell: runbook de script de PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="08cb7-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="08cb7-135">GraphPowerShellWorkflow: runbook de flujo de trabajo de PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="08cb7-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="08cb7-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="08cb7-136">logProgress</span></span> |<span data-ttu-id="08cb7-137">Especifica si se deben generar [registros de progreso](../automation/automation-runbook-output-and-messages.md) para el runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="08cb7-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="08cb7-138">logVerbose</span></span> |<span data-ttu-id="08cb7-139">Especifica si se deben generar [registros detallados](../automation/automation-runbook-output-and-messages.md) para el runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="08cb7-140">Description</span><span class="sxs-lookup"><span data-stu-id="08cb7-140">description</span></span> |<span data-ttu-id="08cb7-141">Descripción opcional del runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="08cb7-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="08cb7-142">publishContentLink</span></span> |<span data-ttu-id="08cb7-143">Especifica el contenido del runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="08cb7-144">uri: URI del contenido del runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="08cb7-145">Será un archivo. ps1 para los runbooks de PowerShell y script, y un archivo de runbook gráfico exportado para un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="08cb7-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="08cb7-146">version: versión del runbook para su propio seguimiento.</span><span class="sxs-lookup"><span data-stu-id="08cb7-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="08cb7-147">Trabajos de automatización</span><span class="sxs-lookup"><span data-stu-id="08cb7-147">Automation jobs</span></span>
<span data-ttu-id="08cb7-148">Cuando se inicia un runbook en Azure Automation, se crea un trabajo de automatización.</span><span class="sxs-lookup"><span data-stu-id="08cb7-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="08cb7-149">Puede agregar un recurso de trabajo de automatización a la solución para iniciar un runbook automáticamente al instalarse la solución de administración.</span><span class="sxs-lookup"><span data-stu-id="08cb7-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="08cb7-150">Este método se suele usar para iniciar runbooks que se emplean para la configuración inicial de la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="08cb7-151">Para iniciar un runbook a intervalos regulares, cree una [programación](#schedules) y un [programa de trabajos](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="08cb7-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="08cb7-152">Los recursos de trabajo tienen un tipo de **Microsoft.Automation/automationAccounts/jobs** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="08cb7-153">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="08cb7-154">En la tabla siguiente se describen las propiedades para los trabajos de automatización.</span><span class="sxs-lookup"><span data-stu-id="08cb7-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="08cb7-155">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-155">Property</span></span> | <span data-ttu-id="08cb7-156">Description</span><span class="sxs-lookup"><span data-stu-id="08cb7-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-157">runbook</span><span class="sxs-lookup"><span data-stu-id="08cb7-157">runbook</span></span> |<span data-ttu-id="08cb7-158">Entidad name única con el nombre del runbook que se va a iniciar.</span><span class="sxs-lookup"><span data-stu-id="08cb7-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="08cb7-159">parameters</span><span class="sxs-lookup"><span data-stu-id="08cb7-159">parameters</span></span> |<span data-ttu-id="08cb7-160">Entidad de cada valor del parámetro que necesita el runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="08cb7-161">El trabajo incluye el nombre del runbook y los valores de los parámetros que se deben enviar al runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="08cb7-162">El trabajo debe [depender del](operations-management-suite-solutions-solution-file.md#resources) runbook que se inicia, ya que el runbook debe crearse antes del trabajo.</span><span class="sxs-lookup"><span data-stu-id="08cb7-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="08cb7-163">Si tiene varios runbooks que deben iniciarse, puede definir su orden teniendo un trabajo dependiente de cualquier otro trabajo que deba ejecutarse primero.</span><span class="sxs-lookup"><span data-stu-id="08cb7-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="08cb7-164">El nombre de un recurso de trabajo debe contener un GUID que suele asignar un parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="08cb7-165">Puede obtener más información sobre los parámetros GUID en [Creating solutions in Operations Management Suite (OMS) (Creación de soluciones en Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="08cb7-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="08cb7-166">Certificados</span><span class="sxs-lookup"><span data-stu-id="08cb7-166">Certificates</span></span>
<span data-ttu-id="08cb7-167">Los [certificados de Azure Automation](../automation/automation-certificates.md) tienen un tipo de **Microsoft.Automation/automationAccounts/certificates** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="08cb7-168">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="08cb7-169">En la tabla siguiente se describen las propiedades para los recursos de certificados.</span><span class="sxs-lookup"><span data-stu-id="08cb7-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="08cb7-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-170">Property</span></span> | <span data-ttu-id="08cb7-171">Description</span><span class="sxs-lookup"><span data-stu-id="08cb7-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="08cb7-172">base64Value</span></span> |<span data-ttu-id="08cb7-173">Valor Base 64 del certificado.</span><span class="sxs-lookup"><span data-stu-id="08cb7-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="08cb7-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="08cb7-174">thumbprint</span></span> |<span data-ttu-id="08cb7-175">Huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="08cb7-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="08cb7-176">Credenciales</span><span class="sxs-lookup"><span data-stu-id="08cb7-176">Credentials</span></span>
<span data-ttu-id="08cb7-177">Las [credenciales de Azure Automation](../automation/automation-credentials.md) tienen un tipo de **Microsoft.Automation/automationAccounts/credentials** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="08cb7-178">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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

<span data-ttu-id="08cb7-179">En la tabla siguiente se describen las propiedades para los recursos de credenciales.</span><span class="sxs-lookup"><span data-stu-id="08cb7-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="08cb7-180">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-180">Property</span></span> | <span data-ttu-id="08cb7-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="08cb7-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-182">userName</span><span class="sxs-lookup"><span data-stu-id="08cb7-182">userName</span></span> |<span data-ttu-id="08cb7-183">Nombre de usuario de la credencial.</span><span class="sxs-lookup"><span data-stu-id="08cb7-183">User name for the credential.</span></span> |
| <span data-ttu-id="08cb7-184">contraseña</span><span class="sxs-lookup"><span data-stu-id="08cb7-184">password</span></span> |<span data-ttu-id="08cb7-185">Contraseña de la credencial.</span><span class="sxs-lookup"><span data-stu-id="08cb7-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="08cb7-186">Programaciones</span><span class="sxs-lookup"><span data-stu-id="08cb7-186">Schedules</span></span>
<span data-ttu-id="08cb7-187">Las [programaciones de Azure Automation](../automation/automation-schedules.md) tienen un tipo de **Microsoft.Automation/automationAccounts/schedules** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="08cb7-188">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="08cb7-189">En la tabla siguiente se describen las propiedades para los recursos de programación.</span><span class="sxs-lookup"><span data-stu-id="08cb7-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="08cb7-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-190">Property</span></span> | <span data-ttu-id="08cb7-191">Descripción</span><span class="sxs-lookup"><span data-stu-id="08cb7-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-192">Description</span><span class="sxs-lookup"><span data-stu-id="08cb7-192">description</span></span> |<span data-ttu-id="08cb7-193">Descripción opcional de la programación.</span><span class="sxs-lookup"><span data-stu-id="08cb7-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="08cb7-194">startTime</span><span class="sxs-lookup"><span data-stu-id="08cb7-194">startTime</span></span> |<span data-ttu-id="08cb7-195">Especifica la hora de inicio de una programación como un objeto DateTime.</span><span class="sxs-lookup"><span data-stu-id="08cb7-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="08cb7-196">Se puede proporcionar una cadena si esta se puede convertir en un valor DateTime válido.</span><span class="sxs-lookup"><span data-stu-id="08cb7-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="08cb7-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="08cb7-197">isEnabled</span></span> |<span data-ttu-id="08cb7-198">Especifica si la programación está habilitada.</span><span class="sxs-lookup"><span data-stu-id="08cb7-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="08cb7-199">interval</span><span class="sxs-lookup"><span data-stu-id="08cb7-199">interval</span></span> |<span data-ttu-id="08cb7-200">El tipo de intervalo de la programación.</span><span class="sxs-lookup"><span data-stu-id="08cb7-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="08cb7-201">day</span><span class="sxs-lookup"><span data-stu-id="08cb7-201">day</span></span><br><span data-ttu-id="08cb7-202">hour</span><span class="sxs-lookup"><span data-stu-id="08cb7-202">hour</span></span> |
| <span data-ttu-id="08cb7-203">frequency</span><span class="sxs-lookup"><span data-stu-id="08cb7-203">frequency</span></span> |<span data-ttu-id="08cb7-204">Frecuencia con la que la programación se debe activar en cantidad de días u horas.</span><span class="sxs-lookup"><span data-stu-id="08cb7-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="08cb7-205">Las programaciones deben tener una hora de inicio con un valor mayor que la hora actual.</span><span class="sxs-lookup"><span data-stu-id="08cb7-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="08cb7-206">No puede proporcionar este valor con una variable, ya que no tendría forma de saber cuándo se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="08cb7-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="08cb7-207">Use una de las dos estrategias siguientes al usar recursos de programación en una solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="08cb7-208">Use un parámetro para la hora de inicio de la programación.</span><span class="sxs-lookup"><span data-stu-id="08cb7-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="08cb7-209">Este pedirá al usuario que proporcione un valor cuando instale la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="08cb7-210">Si tiene varias programaciones, podría usar un valor del parámetro único para más de una.</span><span class="sxs-lookup"><span data-stu-id="08cb7-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="08cb7-211">Cree las programaciones mediante un runbook que se inicie al instalarse la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="08cb7-212">De este modo, ya no es necesario que el usuario especifique una hora, pero usted no puede contener la programación en su solución, por lo que se quitará al quitarse también la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="08cb7-213">Programaciones del trabajo</span><span class="sxs-lookup"><span data-stu-id="08cb7-213">Job schedules</span></span>
<span data-ttu-id="08cb7-214">Los recursos de programación de trabajo vinculan un runbook con una programación.</span><span class="sxs-lookup"><span data-stu-id="08cb7-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="08cb7-215">Tienen un tipo de **Microsoft.Automation/automationAccounts/jobSchedules** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="08cb7-216">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="08cb7-217">En la tabla siguiente se describen las propiedades para las programaciones de trabajo.</span><span class="sxs-lookup"><span data-stu-id="08cb7-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="08cb7-218">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-218">Property</span></span> | <span data-ttu-id="08cb7-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="08cb7-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-220">nombre de programación</span><span class="sxs-lookup"><span data-stu-id="08cb7-220">schedule name</span></span> |<span data-ttu-id="08cb7-221">Entidad **name** única con el nombre de la programación.</span><span class="sxs-lookup"><span data-stu-id="08cb7-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="08cb7-222">nombre de runbook</span><span class="sxs-lookup"><span data-stu-id="08cb7-222">runbook name</span></span>  |<span data-ttu-id="08cb7-223">Entidad **name** única con el nombre del runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="08cb7-224">Variables</span><span class="sxs-lookup"><span data-stu-id="08cb7-224">Variables</span></span>
<span data-ttu-id="08cb7-225">Las [variables de Azure Automation](../automation/automation-variables.md) tienen un tipo de **Microsoft.Automation/automationAccounts/variables** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="08cb7-226">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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

<span data-ttu-id="08cb7-227">En la tabla siguiente se describen las propiedades para los recursos de variables.</span><span class="sxs-lookup"><span data-stu-id="08cb7-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="08cb7-228">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-228">Property</span></span> | <span data-ttu-id="08cb7-229">Descripción</span><span class="sxs-lookup"><span data-stu-id="08cb7-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-230">Description</span><span class="sxs-lookup"><span data-stu-id="08cb7-230">description</span></span> | <span data-ttu-id="08cb7-231">Descripción opcional de la variable.</span><span class="sxs-lookup"><span data-stu-id="08cb7-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="08cb7-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="08cb7-232">isEncrypted</span></span> | <span data-ttu-id="08cb7-233">Especifica si se debe cifrar la variable.</span><span class="sxs-lookup"><span data-stu-id="08cb7-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="08cb7-234">type</span><span class="sxs-lookup"><span data-stu-id="08cb7-234">type</span></span> | <span data-ttu-id="08cb7-235">Esta propiedad no tiene actualmente ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="08cb7-235">This property currently has no effect.</span></span>  <span data-ttu-id="08cb7-236">El tipo de datos de la variable se determinará por el valor inicial.</span><span class="sxs-lookup"><span data-stu-id="08cb7-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="08cb7-237">value</span><span class="sxs-lookup"><span data-stu-id="08cb7-237">value</span></span> | <span data-ttu-id="08cb7-238">Valor de la variable.</span><span class="sxs-lookup"><span data-stu-id="08cb7-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="08cb7-239">La propiedad **type** no tiene actualmente ningún efecto en la variable que se está creando.</span><span class="sxs-lookup"><span data-stu-id="08cb7-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="08cb7-240">El tipo de datos de la variable se determinará por el valor.</span><span class="sxs-lookup"><span data-stu-id="08cb7-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="08cb7-241">Si establece el valor inicial de la variable, este debe configurarse con el tipo de datos correcto.</span><span class="sxs-lookup"><span data-stu-id="08cb7-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="08cb7-242">La tabla siguiente muestra los tipos de datos permitidos y su sintaxis.</span><span class="sxs-lookup"><span data-stu-id="08cb7-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="08cb7-243">Tenga en cuenta que es previsible que los valores en formato JSON vayan siempre entre comillas, incluyendo todos los caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="08cb7-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="08cb7-244">Por ejemplo, un valor de cadena se especificaría con comillas alrededor de la cadena (mediante el carácter de escape [\\]) mientras que un valor numérico se especificaría con un conjunto de comillas.</span><span class="sxs-lookup"><span data-stu-id="08cb7-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="08cb7-245">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="08cb7-245">Data type</span></span> | <span data-ttu-id="08cb7-246">Descripción</span><span class="sxs-lookup"><span data-stu-id="08cb7-246">Description</span></span> | <span data-ttu-id="08cb7-247">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="08cb7-247">Example</span></span> | <span data-ttu-id="08cb7-248">Se resuelve como</span><span class="sxs-lookup"><span data-stu-id="08cb7-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="08cb7-249">cadena</span><span class="sxs-lookup"><span data-stu-id="08cb7-249">string</span></span>   | <span data-ttu-id="08cb7-250">Incluya el valor entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="08cb7-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="08cb7-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="08cb7-251">"\"Hello world\""</span></span> | <span data-ttu-id="08cb7-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="08cb7-252">"Hello world"</span></span> |
| <span data-ttu-id="08cb7-253">numeric</span><span class="sxs-lookup"><span data-stu-id="08cb7-253">numeric</span></span>  | <span data-ttu-id="08cb7-254">Valor numérico con comillas simples.</span><span class="sxs-lookup"><span data-stu-id="08cb7-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="08cb7-255">"64"</span><span class="sxs-lookup"><span data-stu-id="08cb7-255">"64"</span></span> | <span data-ttu-id="08cb7-256">64</span><span class="sxs-lookup"><span data-stu-id="08cb7-256">64</span></span> |
| <span data-ttu-id="08cb7-257">boolean</span><span class="sxs-lookup"><span data-stu-id="08cb7-257">boolean</span></span>  | <span data-ttu-id="08cb7-258">**true** o **false** entre comillas.</span><span class="sxs-lookup"><span data-stu-id="08cb7-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="08cb7-259">Tenga en cuenta que este valor debe ir en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="08cb7-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="08cb7-260">"true"</span><span class="sxs-lookup"><span data-stu-id="08cb7-260">"true"</span></span> | <span data-ttu-id="08cb7-261">true</span><span class="sxs-lookup"><span data-stu-id="08cb7-261">true</span></span> |
| <span data-ttu-id="08cb7-262">datetime</span><span class="sxs-lookup"><span data-stu-id="08cb7-262">datetime</span></span> | <span data-ttu-id="08cb7-263">Valor de fecha serializado.</span><span class="sxs-lookup"><span data-stu-id="08cb7-263">Serialized date value.</span></span><br><span data-ttu-id="08cb7-264">Puede usar el cmdlet ConvertTo-Json de PowerShell para generar este valor para una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="08cb7-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="08cb7-265">Ejemplo: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="08cb7-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="08cb7-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="08cb7-266">ConvertTo-Json</span></span> | <span data-ttu-id="08cb7-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="08cb7-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="08cb7-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="08cb7-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="08cb7-269">Módulos</span><span class="sxs-lookup"><span data-stu-id="08cb7-269">Modules</span></span>
<span data-ttu-id="08cb7-270">La solución de administración no necesita definir los [módulos globales](../automation/automation-integration-modules.md) que usan los runbooks porque siempre estarán disponibles en la cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="08cb7-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="08cb7-271">Debe incluir un recurso para cualquier otro módulo usado por los runbooks.</span><span class="sxs-lookup"><span data-stu-id="08cb7-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="08cb7-272">Los [módulos de integración](../automation/automation-integration-modules.md) tienen un tipo de **Microsoft.Automation/automationAccounts/modules** y tienen la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="08cb7-273">Aquí se incluyen las variables y los parámetros habituales para que pueda copiar y pegar este fragmento de código en su archivo de solución y cambiar los nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="08cb7-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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


<span data-ttu-id="08cb7-274">En la tabla siguiente se describen las propiedades para los recursos de módulos.</span><span class="sxs-lookup"><span data-stu-id="08cb7-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="08cb7-275">Propiedad</span><span class="sxs-lookup"><span data-stu-id="08cb7-275">Property</span></span> | <span data-ttu-id="08cb7-276">Descripción</span><span class="sxs-lookup"><span data-stu-id="08cb7-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08cb7-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="08cb7-277">contentLink</span></span> |<span data-ttu-id="08cb7-278">Especifica el contenido del módulo.</span><span class="sxs-lookup"><span data-stu-id="08cb7-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="08cb7-279">uri: URI del contenido del módulo.</span><span class="sxs-lookup"><span data-stu-id="08cb7-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="08cb7-280">Será un archivo. ps1 para los runbooks de PowerShell y script, y un archivo de runbook gráfico exportado para un runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="08cb7-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="08cb7-281">version: versión del módulo para su propio seguimiento.</span><span class="sxs-lookup"><span data-stu-id="08cb7-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="08cb7-282">El runbook debe depender del recurso de módulos para garantizar que se cree antes que el runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="08cb7-283">Actualización de módulos</span><span class="sxs-lookup"><span data-stu-id="08cb7-283">Updating modules</span></span>
<span data-ttu-id="08cb7-284">Si actualiza una solución de administración que incluye un runbook que usa una programación y la nueva versión de la solución tiene un nuevo módulo que usa ese runbook, el runbook puede usar la versión anterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="08cb7-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="08cb7-285">Debe incluir los siguientes runbooks en la solución y crear un trabajo para ejecutarlos antes que cualquier otro runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="08cb7-286">Así se asegurará de que todos los módulos se actualizan según sea necesario antes de que se carguen los runbooks.</span><span class="sxs-lookup"><span data-stu-id="08cb7-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="08cb7-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) garantizará que la versión de todos los módulos que usan los runbooks en la solución sea la más reciente.</span><span class="sxs-lookup"><span data-stu-id="08cb7-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="08cb7-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) volverá a registrar todos los recursos de programación para asegurarse de que los runbooks vinculados a ellos usen los módulos más recientes.</span><span class="sxs-lookup"><span data-stu-id="08cb7-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="08cb7-289">Muestra</span><span class="sxs-lookup"><span data-stu-id="08cb7-289">Sample</span></span>
<span data-ttu-id="08cb7-290">A continuación se muestra un ejemplo de una solución que incluye los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="08cb7-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="08cb7-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="08cb7-291">Runbook.</span></span>  <span data-ttu-id="08cb7-292">Este es un runbook de ejemplo almacenado en un repositorio de GitHub público.</span><span class="sxs-lookup"><span data-stu-id="08cb7-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="08cb7-293">Trabajo de automatización que inicia el runbook cuando se instala la solución.</span><span class="sxs-lookup"><span data-stu-id="08cb7-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="08cb7-294">Programación y programa de trabajos para iniciar el runbook a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="08cb7-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="08cb7-295">Certificado.</span><span class="sxs-lookup"><span data-stu-id="08cb7-295">Certificate.</span></span>
- <span data-ttu-id="08cb7-296">Credencial.</span><span class="sxs-lookup"><span data-stu-id="08cb7-296">Credential.</span></span>
- <span data-ttu-id="08cb7-297">Variable.</span><span class="sxs-lookup"><span data-stu-id="08cb7-297">Variable.</span></span>
- <span data-ttu-id="08cb7-298">Módulo.</span><span class="sxs-lookup"><span data-stu-id="08cb7-298">Module.</span></span>  <span data-ttu-id="08cb7-299">Este es el [módulo OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) para escribir datos en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="08cb7-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="08cb7-300">En el ejemplo se utilizan variables de [parámetros de solución estándar](operations-management-suite-solutions-solution-file.md#parameters) que se suelen utilizar en una solución en lugar de codificar valores en las definiciones de recursos.</span><span class="sxs-lookup"><span data-stu-id="08cb7-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


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
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="08cb7-301">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08cb7-301">Next steps</span></span>
* <span data-ttu-id="08cb7-302">[Agregar una vista a la solución](operations-management-suite-solutions-resources-views.md) para visualizar los datos recopilados.</span><span class="sxs-lookup"><span data-stu-id="08cb7-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
