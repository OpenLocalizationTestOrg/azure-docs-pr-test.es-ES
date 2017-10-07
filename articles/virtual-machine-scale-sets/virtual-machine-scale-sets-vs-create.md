---
title: "aaaDeploy conjunto de escala de máquinas virtuales con Visual Studio | Documentos de Microsoft"
description: "Implementación de un conjunto de escalado de máquinas virtuales mediante Visual Studio y una plantilla de Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>¿Cómo toocreate configuración de escalas de máquina Virtual con Visual Studio
Este artículo muestra cómo toodeploy en que una escala de máquinas virtuales de Azure establecido de mediante una implementación de grupo de recursos de Visual Studio.

[Conjuntos de escalas de máquina Virtual de Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) es un toodeploy de recursos de proceso de Azure y administrar una colección de máquinas virtuales similares con escala automática y el equilibrio de carga. Puede aprovisionar e implementar conjuntos de escalado de máquinas virtuales mediante [plantillas de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates). Las plantillas de Azure Resource Manager se pueden implementar mediante la CLI de Azure, PowerShell, REST y también directamente desde Visual Studio. Visual Studio proporciona un conjunto de plantillas que se pueden implementar como parte de un proyecto de implementación de grupo de recursos de Azure.

Las implementaciones de grupo de recursos de Azure son una manera toogroup y publican un conjunto de recursos de Azure relacionados en una única operación de implementación. Puede obtener más información aquí: [Creación e implementación de grupos de recursos de Azure mediante Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="pre-requisites"></a>Requisitos previos
tooget introducción sobre cómo implementar conjuntos de escalas de máquina Virtual en Visual Studio, necesita siguiente de hello:

* Visual Studio 2013 o posterior.
* Azure SDK 2.7, 2.8 o 2.9

>[!NOTE]
>En estas instrucciones se asume que usa Visual Studio con el [SDK de Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Creación de un proyecto
1. Cree un proyecto nuevo en Visual Studio; para ello, seleccione **Archivo | Nuevo | Proyecto**.
   
    ![Archivo nuevo][file_new]

2. En **Visual C# | En la nube**, elija **Azure Resource Manager** toocreate un proyecto para la implementación de una plantilla de administrador de recursos de Azure.
   
    ![Crear proyecto][create_project]

3. En lista de Hola de plantillas, seleccione Hola Linux o plantilla de conjunto de escala de máquina Virtual de Windows.
   
   ![Seleccionar plantilla][select_Template]

4. Una vez creado el proyecto verá scripts de implementación de PowerShell, una plantilla de administrador de recursos de Azure y un archivo de parámetros para hello conjunto de escala de máquinas virtuales.
   
    ![Explorador de soluciones][solution_explorer]

## <a name="customize-your-project"></a>Personalización del proyecto
Ahora puede editar Hola plantilla toocustomize para las necesidades de su aplicación, como agregar propiedades de extensión de máquina virtual o de edición cargar reglas del equilibrio. De forma predeterminada plantillas de conjunto de escala de máquina Virtual de hello son toodeploy configurado hello AzureDiagnostics extensión, lo cual resulta fácil tooadd reglas de escalado automático. También implementa un equilibrador de carga con una dirección IP pública, configurado con reglas NAT entrantes. 

equilibrador de carga de Hello le permite conectarse toohello instancias de máquina virtual con SSH (Linux) o RDP (Windows). intervalo de puertos front-end de Hello comienza en 50000. Para linux, esto significa que si se SSH tooport 50000, está enrutado tooport 22 de Hola primera VM Hola conjunto de escalado. Conexión tooport 50001 es enrutado tooport 22 de hello segunda máquina virtual y así sucesivamente.

 Una buena manera tooedit las plantillas de Visual Studio es toouse Hola esquema JSON tooorganize Hola parámetros, variables y recursos. Con una comprensión de hello esquema Visual Studio puede señalar errores en la plantilla antes de implementarlo.

![Explorador de JSON][json_explorer]

## <a name="deploy-hello-project"></a>Implementar proyecto de Hola
1. Implementar el recurso de conjunto de escala de máquinas virtuales de hello plantilla del Administrador de recursos de Azure toocreate Hola. Haga doble clic en el nodo del proyecto de Hola y elija **implementar | Nueva implementación**.
   
    ![Implementar plantilla][5deploy_Template]
    
2. Seleccione la suscripción en el cuadro de diálogo de Hola "Implementar tooResource grupo".
   
    ![Implementar plantilla][6deploy_Template]

3. Desde aquí, puede crear la plantilla para un toodeploy de grupo de recursos de Azure.
   
    ![Nuevo grupo de recursos][new_resource]

4. A continuación, haga clic en **editar parámetros** tooenter parámetros que se pasan tooyour plantilla. Proporcionar Hola username y password para hello OS, que es la implementación de hello toocreate necesarios. Si no tiene las herramientas de PowerShell para Visual Studio instalado, se recomienda toocheck **guardar contraseñas** tooavoid un línea de comandos de PowerShell oculto solicitar o usar [keyvault compatibilidad](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Editar parámetros][edit_parameters]

5. Ahora haga clic en **Implementar**. Hola **salida** ventana muestra el progreso de la implementación de Hola. Tenga en cuenta que la acción de Hola se está ejecutando hello **Deploy-AzureResourceGroup.ps1** secuencia de comandos.
   
   ![Ventana de salida][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>Exploración del conjunto de escalado de máquinas virtuales
Una vez que se haya completado la implementación de hello, puede ver Hola conjunto escala de máquinas virtuales nuevas en Visual Studio hello **nube explorador** (lista de Hola de actualización). Cloud Explorer le permite administrar recursos de Azure en Visual Studio mientras se desarrollan aplicaciones. También puede ver el conjunto de escala de máquinas virtuales en hello [portal de Azure](https://portal.azure.com) y [Explorador de recursos de Azure](https://resources.azure.com/).

![Cloud Explorer][cloud_explorer]

 portal de Hello proporciona la mejor manera de hello toovisually administrar su infraestructura de Azure con un explorador web, mientras que el Explorador de recursos de Azure proporciona una manera sencilla de tooexplore y depurar recursos de Azure, lo que proporciona una ventana en Hola "instancia ver" y muestra PowerShell comandos para los recursos de Hola que está mirando.

## <a name="next-steps"></a>Pasos siguientes
Una vez que haya implementado correctamente conjuntos de escalas de máquina Virtual a través de Visual Studio, se pueden personalizar aún más su proyecto toosuit requisitos de su aplicación. Por ejemplo, configurar la escala automática mediante la adición de un **visión** recursos, agregar tooyour plantilla de infraestructura (por ejemplo, VM independientes), o implementar las aplicaciones que usan la extensión de script personalizado de Hola. Plantillas de buen ejemplo pueden encontrarse en hello [plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) repositorio de GitHub (busque "vmss").

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
