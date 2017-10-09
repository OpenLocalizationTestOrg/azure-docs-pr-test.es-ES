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
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Agregar la solución de administración de automatización de Azure recursos tooan OMS (versión preliminar)
> [!NOTE]
> La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar. Cualquier esquema que se describe a continuación es toochange de asunto.   


[Soluciones de administración de OMS](operations-management-suite-solutions.md) incluirá, normalmente runbooks en automatización de Azure tooautomate procesos como recopilar y procesar datos de supervisión.  Además toorunbooks, cuentas de automatización incluye activos como variables y las programaciones que admiten runbooks hello usa en soluciones de Hola.  Este artículo se describe cómo tooinclude runbooks y sus recursos relacionados en una solución.

> [!NOTE]
> Hello ejemplos en este artículo usan parámetros y variables que están bien soluciones toomanagement necesarias o habituales y se describen en [crear soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que ya está familiarizado con hello siguiente información.

- Cómo demasiado[crear una solución de administración](operations-management-suite-solutions-creating.md).
- Hola la estructura de un [archivo de solución](operations-management-suite-solutions-solution-file.md).
- Cómo demasiado[crear plantillas de administrador de recursos](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Cuenta de Automation
Todos los recursos de Azure Automation están incluidos en una [cuenta de Automation](../automation/automation-security-overview.md#automation-account-overview).  Como se describe en [OMS área de trabajo y la cuenta de automatización](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Hola cuenta de automatización no se incluye en la solución de administración de hello, pero debe existir antes de instala la solución de Hola.  Si no está disponible, se producirá un error en la instalación de la solución de Hola.

nombre de Hola de cada recurso de automatización incluye Hola de su cuenta de automatización.  Esto se hace en soluciones de hello con hello **accountName** parámetro como en el siguiente ejemplo de un recurso de runbook de Hola.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbooks
Debe incluir los runbooks utilizados por solución de hello en el archivo de solución de Hola para que se crean cuando se instala la solución de Hola.  No puede contener cuerpo Hola de runbook de hello en la plantilla de hello aunque, por lo que debe publicar Hola runbook tooa ubicación pública a la que puede obtenerse por cualquier usuario que instala la solución.

[Runbook de automatización de Azure](../automation/automation-runbook-types.md) recursos tienen un tipo de **Microsoft.Automation/automationAccounts/runbooks** y tener Hola siguiendo la estructura. Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 

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


propiedades de Hola de runbooks se describen en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| runbookType |Especifica los tipos de Hola de runbook de Hola. <br><br> Script: script de PowerShell <br>PowerShell: flujo de trabajo de PowerShell <br> GraphPowerShell: runbook de script de PowerShell gráfico <br> GraphPowerShellWorkflow: runbook de flujo de trabajo de PowerShell gráfico |
| logProgress |Especifica si [registros de progreso](../automation/automation-runbook-output-and-messages.md) para hello runbook debe generarse. |
| logVerbose |Especifica si [registros detallados](../automation/automation-runbook-output-and-messages.md) para hello runbook debe generarse. |
| description |Descripción opcional para el runbook de Hola. |
| publishContentLink |Especifica el contenido de Hola de runbook de Hola. <br><br>URI - Uri toohello contenido de runbook de Hola.  Será un archivo. ps1 para los runbooks de PowerShell y script, y un archivo de runbook gráfico exportado para un runbook gráfico.  <br> versión: versión de runbook de Hola para su propio seguimiento. |


## <a name="automation-jobs"></a>Trabajos de automatización
Cuando se inicia un runbook en Azure Automation, se crea un trabajo de automatización.  Puede agregar un inicio de tooautomatically la automatización de la tarea recursos tooyour solución un runbook cuando se instala la solución de administración de Hola.  Este método es toostart normalmente se usan runbooks que se usan para la configuración inicial de solución de Hola.  crear un runbook a intervalos regulares, toostart una [programación](#schedules) y un [la programación del trabajo](#job-schedules)

Recursos de trabajo tienen un tipo de **Microsoft.Automation/automationAccounts/jobs** y tener Hola siguiendo la estructura.  Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 

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

propiedades de Hola para trabajos de automatización se describen en hello en la tabla siguiente.

| Propiedad | Description |
|:--- |:--- |
| runbook |Entidad de nombre único con el nombre de Hola de hello runbook toostart. |
| parameters |Entidad de cada valor de parámetro requerido por runbook Hola. |

trabajo de Hello incluye el nombre de runbook de Hola y cualquier toobe de valores de parámetro enviado toohello runbook.  trabajo de Hello debe [dependen](operations-management-suite-solutions-solution-file.md#resources) Hola runbook que se está iniciando desde runbook Hola debe crearse antes de trabajo de Hola.  Si tiene varios runbooks que deben iniciarse, puede definir su orden teniendo un trabajo dependiente de cualquier otro trabajo que deba ejecutarse primero.

nombre de Hola de un recurso de trabajo debe contener un GUID que se asigna normalmente por un parámetro.  Puede obtener más información sobre los parámetros GUID en [Creating solutions in Operations Management Suite (OMS) (Creación de soluciones en Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Certificados
[Certificados de automatización de Azure](../automation/automation-certificates.md) tienen un tipo de **Microsoft.Automation/automationAccounts/certificates** y tener Hola siguiendo la estructura. Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 

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



propiedades de Hola de recursos de certificados se describen en hello en la tabla siguiente.

| Propiedad | Description |
|:--- |:--- |
| base64Value |Valor de base 64 para el certificado de Hola. |
| thumbprint |Huella digital de certificado de Hola. |



## <a name="credentials"></a>Credenciales
[Credenciales de automatización de Azure](../automation/automation-credentials.md) tienen un tipo de **Microsoft.Automation/automationAccounts/credentials** y tener Hola siguiendo la estructura.  Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 


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

propiedades de Hola de recursos de la credencial se describen en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| userName |Nombre de usuario para las credenciales de Hola. |
| Contraseña |Contraseña de la credencial de Hola. |


## <a name="schedules"></a>Programaciones
[Programaciones de automatización de Azure](../automation/automation-schedules.md) tienen un tipo de **Microsoft.Automation/automationAccounts/schedules** y tener Hola Hola siguiendo la estructura. Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 

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

propiedades de Hola para programar los recursos se describen en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| description |Descripción opcional para la programación de Hola. |
| startTime |Especifica la hora de inicio de Hola de una programación como un objeto DateTime. Puede proporcionar una cadena si se puede convertir tooa DateTime válido. |
| isEnabled |Especifica si está habilitada la programación de Hola. |
| interval |tipo de Hola de intervalo de programación de Hola.<br><br>day<br>hour |
| frequency |Frecuencia con la que Hola programación debería desencadenar en número de días u horas. |

Programa debe tener una hora de inicio con un valor mayor que Hola hora actual.  No puede proporcionar este valor con una variable, ya que no tendría ninguna manera de saber si se trata de toobe va instalado.

Utilice uno de hello siguiendo dos estrategias al usar recursos de programación en una solución.

- Usar un parámetro de hora de inicio de Hola de programación de Hola.  Al instalar soluciones de hello, se le pedirá Hola usuario tooprovide un valor.  Si tiene varias programaciones, podría usar un valor del parámetro único para más de una.
- Crear programaciones de hello utilizando un runbook que se inicia cuando se instala la solución de Hola.  Esto elimina la necesidad de Hola de hello toospecify de usuario una vez, pero no puede contener programación hello en la solución, por lo que se quitarán cuando se quita la solución de Hola.


### <a name="job-schedules"></a>Programaciones del trabajo
Los recursos de programación de trabajo vinculan un runbook con una programación.  Tienen un tipo de **Microsoft.Automation/automationAccounts/jobSchedules** y tener Hola Hola siguiendo la estructura.  Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 

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


en hello en la tabla siguiente se describen propiedades de Hola para las programaciones de trabajo.

| Propiedad | Descripción |
|:--- |:--- |
| nombre de programación |Solo **nombre** entidad con el nombre de Hola de programación de Hola. |
| nombre de runbook  |Solo **nombre** entidad con el nombre de Hola de runbook de Hola.  |



## <a name="variables"></a>variables
[Variables de automatización de Azure](../automation/automation-variables.md) tienen un tipo de **Microsoft.Automation/automationAccounts/variables** y tener Hola siguiendo la estructura.  Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.

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

propiedades de Hola de variable recursos se describen en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| description | Descripción opcional para la variable de saludo. |
| isEncrypted | Especifica si se debe cifrar la variable de saludo. |
| type | Esta propiedad no tiene actualmente ningún efecto.  tipo de datos de Hola de variable de saludo se determinará por el valor inicial de Hola. |
| value | Valor de variable de saludo. |

> [!NOTE]
> Hola **tipo** propiedad no tiene ningún efecto en la variable de saludo que se está creando.  Hola de tipo de datos para la variable de saludo se determinará por el valor de Hola.  

Si establece el valor inicial de hello para la variable de hello, debe configurarse como tipo de datos correcto de Hola.  Hello en la tabla siguiente proporciona Hola distintos tipos de datos permitidos y su sintaxis.  Tenga en cuenta que los valores de JSON sean tooalways esperado ir entre comillas con los caracteres especiales dentro de las comillas de Hola.  Por ejemplo, un valor de cadena se especificarían por comillas alrededor de la cadena de hello (utilizando el carácter de escape de hello (\\)) mientras se especifica un valor numérico con un conjunto de comillas.

| Tipo de datos | Descripción | Ejemplo | Resuelve demasiado|
|:--|:--|:--|:--|
| cadena   | Incluya el valor entre comillas dobles.  | "\"Hello world\"" | "Hello world" |
| numeric  | Valor numérico con comillas simples.| "64" | 64 |
| boolean  | **true** o **false** entre comillas.  Tenga en cuenta que este valor debe ir en minúsculas. | "true" | true |
| datetime | Valor de fecha serializado.<br>Puede usar este valor de cmdlet ConvertTo-Json de hello en toogenerate de PowerShell para una fecha determinada.<br>Ejemplo: get-date "5/24/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>Módulos
La solución de administración no es necesario toodefine [módulos globales](../automation/automation-integration-modules.md) utilizada por los runbooks ya que siempre estén disponibles en su cuenta de automatización.  Es necesario tooinclude un recurso para cualquier otro módulo utilizado por los runbooks.

[Módulos de integración](../automation/automation-integration-modules.md) tienen un tipo de **Microsoft.Automation/automationAccounts/modules** y tener Hola siguiendo la estructura.  Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola.

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


propiedades de Hola de recursos de módulo se describen en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| contentLink |Especifica el contenido de hello del módulo de Hola. <br><br>URI - Uri toohello contenido del módulo de Hola.  Será un archivo. ps1 para los runbooks de PowerShell y script, y un archivo de runbook gráfico exportado para un runbook gráfico.  <br> versión: versión del módulo de Hola para su propio seguimiento. |

Hola runbook debe depender de hello módulo recursos tooensure que ha creado antes de runbook de Hola.

### <a name="updating-modules"></a>Actualización de módulos
Si actualiza una solución de administración que incluya un runbook que utiliza una programación y Hola nueva versión de la solución tiene un nuevo módulo por ese runbook, Hola runbook puede usar versión anterior de hello del módulo de Hola.  Debe incluir Hola después runbooks en la solución y crear un trabajo toorun automáticamente antes de los otros runbooks.  Esto garantizará que los módulos que se actualizan como Hola necesario antes de cargar los runbooks.

* [Actualización ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) se asegurará de que todos los módulos de hello usan los runbooks en la solución de son la versión más reciente de Hola.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) se vuelva a registrar todas tooensure de recursos de programación Hola que Hola runbooks vinculados toothem con módulos de uso hello más recientes.




## <a name="sample"></a>Muestra
Aquí te mostramos un ejemplo de una solución que incluya incluye Hola recursos siguientes:

- Runbook.  Este es un runbook de ejemplo almacenado en un repositorio de GitHub público.
- Trabajo de automatización que se inicia Hola runbook cuando se instala la solución de Hola.
- Programación y trabajo programación toostart Hola runbook a intervalos regulares.
- Certificado.
- Credencial.
- Variable.
- Módulo.  Se trata de hello [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) para escribir datos tooLog análisis. 

usos de ejemplo de Hola [parámetros de la solución estándar](operations-management-suite-solutions-solution-file.md#parameters) variables que normalmente se utilizarían en una solución como opone toohardcoding valores en las definiciones de recursos de Hola.


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




## <a name="next-steps"></a>Pasos siguientes
* [Agregar una solución de tooyour vista](operations-management-suite-solutions-resources-views.md) toovisualize los datos recopilados.
