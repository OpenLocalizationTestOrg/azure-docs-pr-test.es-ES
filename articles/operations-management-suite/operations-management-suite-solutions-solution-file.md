---
title: "soluciones de administración de aaaCreating en Operations Management Suite (OMS) | Documentos de Microsoft"
description: "Soluciones de administración de amplían la funcionalidad de Hola de Operations Management Suite (OMS) proporcionando escenarios de administración empaquetada que los clientes pueden agregar área de trabajo OMS tootheir.  Este artículo proporciona detalles sobre cómo puede crear toobe de soluciones de administración usan en su propio entorno o estará disponible tooyour clientes."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Creación de archivos de solución de administración en Operations Management Suite (OMS) (versión preliminar)
> [!NOTE]
> La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar. Cualquier esquema que se describe a continuación es toochange de asunto.  

Las soluciones de administración en Operations Management Suite (OMS) se implementan como [plantillas de Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).  la tarea principal Hello para aprender cómo las soluciones de administración de tooauthor es aprender cómo demasiado[crear una plantilla de](../azure-resource-manager/resource-group-authoring-templates.md).  Este artículo proporciona detalles únicos de plantillas que se utilizan para las soluciones y cómo tooconfigure recursos de solución típica.


## <a name="tools"></a>Herramientas

Puede usar cualquier toowork de editor de texto con archivos de solución, pero se recomienda que aprovecha las características de hello proporcionadas en Visual Studio o código de Visual Studio como se describe en los siguientes artículos de Hola.

- [Creación e implementación de grupos de recursos de Azure mediante Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Trabajo con plantillas de Azure Resource Manager en Visual Studio Code](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>sección Estructura
estructura básica de Hola de un archivo de solución de administración es Hola igual que un [plantilla del Administrador de recursos](../azure-resource-manager/resource-group-authoring-templates.md#template-format) que es como se indica a continuación.  Cada uno de hello las siguientes secciones describe los elementos de nivel superior de Hola y y su contenido en una solución.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>parameters
[Parámetros](../azure-resource-manager/resource-group-authoring-templates.md#parameters) son valores que necesita de usuario de hello cuando instala la solución de administración de Hola.  Hay parámetros estándar que tendrán todas las soluciones, y puede agregar parámetros adicionales según sea necesario para su solución particular.  Cómo los usuarios proporcionar valores de parámetro cuando instala la solución dependerá parámetro concreto de Hola y cómo se instala la solución de Hola.

Cuando un usuario instala la solución de administración a través de hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) o [plantillas de inicio rápido de Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) son tooselect solicitada un [OMS área de trabajo y la cuenta de automatización ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Éstos son valores de hello toopopulate utilizadas de cada uno de los parámetros estándar de Hola.  no se solicita el usuario de Hello toodirectly proporcionar valores para parámetros estándar de hello, pero son valores tooprovide solicitadas para cualquier parámetro adicional.

Si instala la solución de usuario de hello [otro método](operations-management-suite-solutions.md#finding-and-installing-management-solutions), debe proporcionar un valor para todos los parámetros estándares y todos los parámetros adicionales.

A continuación se muestra un parámetro de ejemplo.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Hello en la tabla siguiente describe los atributos de Hola de un parámetro.

| Atributo | Descripción |
|:--- |:--- |
| type |Tipo de datos de parámetro hello. control de entrada de Hola que se muestran para el usuario de hello depende de tipo de datos de Hola.<br><br>bool: cuadro desplegable<br>string: cuadro de texto<br>int: cuadro de texto<br>Securestring: campo de contraseña<br> |
| categoría |Categoría opcional para el parámetro hello.  Parámetros en la misma categoría se agrupan de Hola. |
| control |Funcionalidad adicional para los parámetros de cadena.<br><br>datetime: se muestra el control de fecha y hora.<br>GUID - valor Guid se genera automáticamente y no se muestra el parámetro hello. |
| description |Descripción opcional para el parámetro hello.  Se muestran en un parámetro de toohello siguiente de globo de información. |

### <a name="standard-parameters"></a>Parámetros estándar
Hello tabla siguiente enumeran los parámetros estándar de Hola para todas las soluciones de administración.  Estos valores se rellenan para el usuario de hello en lugar de solicitar para ellos cuando se instala la solución de plantillas de Azure Marketplace o inicio rápido de Hola.  usuario de Hello debe proporcionar valores para ellos si se instala la solución de hello con otro método.

> [!NOTE]
> interfaz de usuario de Hello en plantillas de Azure Marketplace y de inicio rápido de hello espera nombres de parámetro de hello en la tabla de Hola.  Si utiliza distintos nombres de parámetro, a continuación, se pedirá usuario Hola para ellos y no se rellenarán automáticamente.
>
>

| Parámetro | Tipo | Descripción |
|:--- |:--- |:--- |
| accountName |string |Nombre de la cuenta de Automation de Azure. |
| pricingTier |string |Plan de tarifa del área de trabajo de Log Analytics y de la cuenta de Automation de Azure. |
| regionId |cadena |Región de hello cuenta de automatización de Azure. |
| solutionName |cadena |Nombre de solución de Hola.  Si va a implementar la solución a través de plantillas de inicio rápido, a continuación, debe definir solutionName como un parámetro para que pueda definir una cadena en su lugar que requieren Hola usuario toospecify uno. |
| workspaceName |string |Nombre del área de trabajo de Log Analytics. |
| workspaceRegionId |cadena |Región del área de trabajo de análisis de registros de Hola. |


Aquí te mostramos estructura Hola de los parámetros estándar de Hola que puede copiar y pegar en el archivo de solución.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


Consulte tooparameter valores de otros elementos de solución de hello con sintaxis de hello **parámetros ('parameter name')**.  Por ejemplo, tooaccess Hola nombre de área de trabajo, usaría **parameters('workspaceName')**

## <a name="variables"></a>variables
[Las variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) son valores que se va a utilizar en el resto de Hola de solución de administración de Hola.  Estos valores no son usuario toohello expuesto instalar Hola solución.  Únicamente son autor de hello tooprovide previsto con una única ubicación que pueden administrar los valores que se pueden usar varias veces a lo largo de la solución de Hola. Debe colocar cualquier solución de tooyour específico de valores en variables como toohard lugar su codificación en hello **recursos** elemento.  Esto hace que el código de hello sea más legible y le permite tooeasily cambiar estos valores en versiones posteriores.

A continuación se muestra un ejemplo del elemento **variables** con parámetros típicos usados en las soluciones.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Consulte toovariable valores a través de la solución de hello con sintaxis de hello **variables ('variable name')**.  Por ejemplo, tooaccess Hola SolutionName variable, usaría **variables('SolutionName')**.

También puede definir variables complejas en varios conjuntos de valores.  Estas son especialmente útiles en soluciones de administración cuando se definen varias propiedades para diferentes tipos de recursos.  Por ejemplo, puede reestructurar las variables de solución de hello mostradas anteriormente toohello siguiente.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

En este caso, consulte toovariable valores a través de la solución de hello con sintaxis de hello **variables('variable name').property**.  Por ejemplo, tooaccess Hola variable de nombre de la solución, usaría **variables('Solution'). Nombre**.

## <a name="resources"></a>Recursos
[Recursos](../azure-resource-manager/resource-group-authoring-templates.md#resources) definen los recursos diferentes de Hola que instalará y configurará la solución de administración.  Se trata de hello más grande y más complejo parte de la plantilla de Hola.  Puede obtener estructura hello y una descripción completa de los elementos de recurso de [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md#resources).  Se detallan distintos recursos que se definirán normalmente en otros artículos en esta documentación. 


### <a name="dependencies"></a>Dependencias
Hola **dependsOn** elementos especifica un [dependencia](../azure-resource-manager/resource-group-define-dependencies.md) en otro recurso.  Cuando se instala la solución de hello, no se crea un recurso hasta que todas sus dependencias se han creado.  Por ejemplo, puede que su solución [inicie un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) cuando se instala mediante un [recurso de trabajo](operations-management-suite-solutions-resources-automation.md#automation-jobs).  recursos de trabajo de Hello sería depende Hola runbook recursos toomake seguro que se crea ese runbook Hola antes de que se crea el trabajo de Hola.

### <a name="oms-workspace-and-automation-account"></a>Área de trabajo de OMS y cuenta de Automation
Las soluciones de administración requieren un [área de trabajo OMS](../log-analytics/log-analytics-manage-access.md) toocontain vistas y una [cuenta de automatización](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks y recursos relacionados.  Estos deben estar disponibles antes de hello recursos de solución de Hola se crean y no deben definirse en la solución de hello propio.  usuario de Hello le [especificar un área de trabajo y una cuenta de](operations-management-suite-solutions.md#oms-workspace-and-automation-account) cuando implementa la solución, pero como autor de hello debe considerar Hola después de puntos.

## <a name="solution-resource"></a>Recursos de solución
Cada solución requiere una entrada de recurso en hello **recursos** elemento que define la propia solución Hola.  Esto tendrá un tipo de **Microsoft.OperationsManagement/solutions** y tener Hola siguiendo la estructura. Esto incluye [parámetros estándar](#parameters) y [variables](#variables) que están toodefine normalmente se usan propiedades de solución de Hola.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Dependencias
recursos de solución de Hello deben tener un [dependencia](../azure-resource-manager/resource-group-define-dependencies.md) en todos los recursos de solución de hello puesto que necesiten tooexist antes de crear una solución de Hola.  Para ello, agrega una entrada para cada recurso en hello **dependsOn** elemento.

### <a name="properties"></a>Propiedades
recursos de solución de Hello tiene propiedades de hello en hello en la tabla siguiente.  Esto incluye recursos de hello al que hace referencia y contenido en la solución de Hola que define cómo se administran los recursos de hello después de instala la solución de Hola.  Cada recurso de solución de hello debe aparecer en cualquier hello **referencedResources** o hello **containedResources** propiedad.

| Propiedad | Descripción |
|:--- |:--- |
| workspaceResourceId |Id. del área de trabajo de análisis de registros de hello en forma de hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nombre de área de trabajo\>*. |
| referencedResources |Lista de recursos de solución de Hola que no se quitan cuando se quita la solución de Hola. |
| containedResources |Lista de recursos de solución de Hola que se deben eliminar cuando se quita la solución de Hola. |

ejemplo de Hola anterior es para una solución con un runbook, una programación y la vista.  programación de Hola y runbook son *que se hace referencia* en hello **propiedades** elemento por lo que no se quitan cuando se quita la solución de Hola.  vista de Hello es *contenidos* por lo que se quita cuando se quita la solución de Hola.

### <a name="plan"></a>Plan
Hola **plan** entidad de recursos de solución de hello tiene propiedades de hello en hello en la tabla siguiente.

| Propiedad | Description |
|:--- |:--- |
| name |Nombre de solución de Hola. |
| versión |Versión de solución de hello según lo determinado por el autor de Hola. |
| product |Solución de hello tooidentify de cadena única. |
| publisher |Publicador de la solución de Hola. |



## <a name="sample"></a>Muestra
Puede ver ejemplos de archivos de solución con un recurso de la solución en hello ubicaciones siguientes.

- [Recursos de Automation](operations-management-suite-solutions-resources-automation.md#sample)
- [Recursos de búsqueda y alerta](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Pasos siguientes
* [Agregar las búsquedas guardadas y alertas](operations-management-suite-solutions-resources-searches-alerts.md) tooyour solución de administración.
* [Agregar vistas](operations-management-suite-solutions-resources-views.md) tooyour solución de administración.
* [Agregar runbooks y otros recursos de automatización](operations-management-suite-solutions-resources-automation.md) tooyour solución de administración.
* Obtenga información acerca de los detalles de Hola de [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md).
* Búsqueda de [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates) para obtener ejemplos de diferentes plantillas de Resource Manager.
