---
title: "aaaViews en soluciones de administración de Operations Management Suite (OMS) | Documentos de Microsoft"
description: "Soluciones de administración de Operations Management Suite (OMS) incluirá, normalmente una o más vistas toovisualize de datos.  En este artículo se describe cómo tooexport una vista creada por hello Diseñador de vistas e incluirla en una solución de administración. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Vistas de las soluciones de administración en Operations Management Suite (OMS) (versión preliminar)
> [!NOTE]
> La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar. Cualquier esquema que se describe a continuación es toochange de asunto.    
>
>

[Soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions.md) incluirá, normalmente una o más vistas toovisualize de datos.  Este artículo describe cómo tooexport una vista creada por hello [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md) e incluirla en una solución de administración.  

> [!NOTE]
> Hello ejemplos en este artículo usan parámetros y variables que están bien soluciones toomanagement necesarias o habituales y se describen en [crear soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que ya está familiarizado con cómo demasiado[crear una solución de administración](operations-management-suite-solutions-creating.md) y la estructura de Hola de un archivo de solución.

## <a name="overview"></a>Información general
tooinclude una vista en una solución de administración, se crea un **recursos** para él en hello [archivo de solución](operations-management-suite-solutions-creating.md).  Hola JSON que describe la configuración detallada de la vista de hello es normalmente complejo aunque y no algo que un autor de la solución típica sería capaz de toocreate manualmente.  Hello método más común es vista de hello toocreate con hello [Diseñador de vistas](../log-analytics/log-analytics-view-designer.md), exportarlo y, a continuación, agregue su solución de toohello de configuración detallada.

pasos básicos de Hello tooadd una solución de tooa de vista son los siguientes.  Cada paso se describe con más detalle en secciones de hello siguientes.

1. Exportar archivo de hello vista tooa.
2. Crear recursos de la vista de hello en soluciones de Hola.
3. Agregar detalles de la vista de Hola.

## <a name="export-hello-view-tooa-file"></a>Exportar archivo de hello vista tooa
Siga las instrucciones de hello en [Diseñador de vistas de análisis de registro](../log-analytics/log-analytics-view-designer.md) tooexport un archivo de tooa de vista.  Hello archivo exportado se puede en formato JSON con Hola mismo [elementos como archivo de solución de hello](operations-management-suite-solutions-solution-file.md).  

Hola **recursos** elemento del archivo de vista de hello tendrá un recurso con un tipo de **Microsoft.OperationalInsights/workspaces** que representa Hola área de trabajo OMS.  Este elemento tiene un elemento secundario con un tipo de **vistas** que representa la vista de Hola y contiene su configuración detallada.  Copiará los detalles de Hola de este elemento y, a continuación, copiarlo en la solución.

## <a name="create-hello-view-resource-in-hello-solution"></a>Crear recursos de la vista de hello en soluciones de Hola
Agregar Hola después de ver recursos toohello **recursos** elemento de su archivo de solución.  Usa las variables que se describen a continuación y que también debe agregar.  Tenga en cuenta que hello **panel** y **OverviewTile** propiedades son marcadores de posición que se sobrescribirá con las propiedades correspondientes del archivo de vista exportada Hola Hola.

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

Agregue Hola siguiente variables toohello variables elemento de archivo de solución de Hola y reemplace toothose de valores de hello para la solución.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Tenga en cuenta que podría copiar recursos de la vista completa de Hola desde el archivo de vista exportada, pero primero necesita hello toomake sigue cambios para toowork en la solución.  

* Hola **tipo** para la vista de hello recurso necesita toobe cambió de **vistas** demasiado**Microsoft.OperationalInsights/workspaces**.
* Hola **nombre** propiedad para el recurso de la vista de hello necesita nombre de área de trabajo de toobe cambiado tooinclude Hola.
* dependencia de Hello en el área de trabajo de hello debe toobe quitado ya recursos del área de trabajo de hello no se ha definido en la solución de Hola.
* **DisplayName** propiedad necesidades toobe agregado toohello vista.  Hola **identificador**, **nombre**, y **DisplayName** debe coincidir.
* Se deben cambiar los nombres de parámetro hello toomatch requiere el conjunto de parámetros.
* Las variables deben definirse en soluciones de Hola y utiliza en las propiedades adecuadas Hola.

## <a name="add-hello-view-details"></a>Agregar detalles de la vista de Hola
recursos de la vista de Hola Hola exportan Vista archivo contendrá dos elementos de hello **propiedades** elemento denominado **panel** y **OverviewTile** que contienen Hola configuración detallada de la vista de Hola.  Copie estos dos elementos y su contenido en hello **propiedades** elemento de recurso de la vista de hello en el archivo de solución.

## <a name="example"></a>Ejemplo
Por ejemplo, hello siguiente ejemplo muestra un archivo de solución sencilla con una vista.  Botón de puntos suspensivos (...) se muestran para hello **panel** y **OverviewTile** contenido por razones de espacio.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a>Pasos siguientes
* Obtener información detallada sobre cómo crear [soluciones de administración](operations-management-suite-solutions-creating.md).
* Incluir [runbooks de Automation en la solución de administración](operations-management-suite-solutions-resources-automation.md).
