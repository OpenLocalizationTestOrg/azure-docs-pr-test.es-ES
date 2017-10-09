---
title: "aaaDeploy un área de trabajo de aprendizaje automático con el Administrador de recursos de Azure | Documentos de Microsoft"
description: "¿Cómo toodeploy un área de trabajo para el aprendizaje automático de Azure mediante la plantilla del Administrador de recursos de Azure"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Implementación del área de trabajo de Machine Learning mediante Azure Resource Manager
## <a name="introduction"></a>Introducción
Mediante una plantilla de implementación guarda en Azure Resource Manager tiempo proporcionando un toodeploy escalable interconectados componentes mediante un mecanismo de validación y vuelva a intentarlo. tooset de áreas de trabajo de aprendizaje de automático de Azure, por ejemplo, necesita toofirst configure una cuenta de almacenamiento de Azure y, a continuación, implementar el área de trabajo. Imagine que tiene que hacer esto manualmente para cientos de áreas de trabajo. Una alternativa más sencilla es toouse un toodeploy de plantilla de Azure Resource Manager un área de trabajo de aprendizaje de automático de Azure y todas sus dependencias. Este artículo le guiará por este proceso paso a paso. Para ver una introducción excelente sobre Azure Resource Manager, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Paso a paso: Creación de un área de trabajo de Machine Learning
Crearemos un grupo de recursos de Azure e implementaremos una nueva cuenta de Almacenamiento de Azure y una nueva área de trabajo de Azure Machine Learning mediante una plantilla de Resource Manager. Una vez completada la implementación de hello, se imprimirá información importante acerca de las áreas de trabajo de hello creados (Hola primary key, workspaceID Hola y el área de trabajo de hello URL toohello).

### <a name="create-an-azure-resource-manager-template"></a>Creación de una plantilla de Azure Resource Manager
Un área de trabajo de aprendizaje automático requiere un tooit de conjunto de datos vinculado de almacenamiento de Azure cuenta toostore Hola.
Hello siguiente plantilla utiliza nombre Hola de nombre de cuenta de almacenamiento de Hola de hello recursos grupo toogenerate y el nombre del área de trabajo de Hola.  También utiliza nombre de cuenta de almacenamiento de hello como una propiedad al crear el área de trabajo de Hola.

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
Guarde esta plantilla como archivo mlworkspace.json en c:\temp.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Implementar grupo de recursos de hello, en función de plantilla de Hola
* Abra PowerShell
* Instale los módulos de Azure Resource Manager y Azure Service Management  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Estos pasos descargar e instalación pasos restantes del Hola Hola módulos toocomplete necesarios. Solo es necesario toobe efectuar una vez en entorno de Hola donde se ejecutan los comandos de PowerShell de Hola.   

* Autenticar tooAzure  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Este paso es necesario toobe repite para cada sesión. Una vez autenticado, aparecerá la información de la suscripción.

![Cuenta de Azure][1]

Ahora que tenemos acceso tooAzure, podemos crear grupo de recursos de Hola.

* Crear un grupo de recursos

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Compruebe que ese grupo de recursos de Hola se aprovisionó correctamente. **ProvisioningState** debe ser "Succeeded" (Correcto).
nombre de grupo de recursos de Hola se usa por nombre de cuenta de almacenamiento de hello plantilla toogenerate Hola. nombre de cuenta de almacenamiento de Hello debe tener entre 3 y 24 caracteres de longitud y usar números y letras en minúsculas solo.

![Grupo de recursos][2]

* Con la implementación del grupo de recursos de hello, implemente una nueva área de trabajo de aprendizaje de máquina.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Una vez completada la implementación de hello, resulta sencillo tooaccess propiedades del área de trabajo de Hola que implementó. Por ejemplo, puede tener acceso a Hola el Token de clave principal.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Otra manera tooretrieve símbolos (tokens) de área de trabajo existente es toouse Hola comando Invoke-AzureRmResourceAction. Por ejemplo, puede enumerar Hola principal y secundaria símbolos (tokens) de todas las áreas de trabajo.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Después de aprovisiona el área de trabajo de hello, también puede automatizar muchas tareas de estudio de aprendizaje automático de Azure con hello [módulo de PowerShell para el aprendizaje automático de Azure](http://aka.ms/amlps).

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre la [creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). 
* Eche un vistazo a hello [repositorio de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates). 
* Vea este vídeo acerca de [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
