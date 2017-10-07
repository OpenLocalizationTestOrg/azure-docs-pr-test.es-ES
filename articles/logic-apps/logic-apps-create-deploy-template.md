---
title: "plantillas de implementación de aaaCreate para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Creación de plantillas de Azure Resource Manager para administrar la implementación y liberación de aplicaciones lógicas"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Creación de plantillas para administrar la implementación y liberación de aplicaciones lógicas

Después de que se ha creado una aplicación de lógica, podría interesarle toocreate como una plantilla de Azure Resource Manager.
De esta manera, puede implementar fácilmente entorno de tooany de aplicaciones de lógica de Hola o grupo de recursos en los que tal vez necesite.
Para obtener más información sobre las plantillas de Resource Manager, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [Implementación de recursos con plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Plantilla de implementación de aplicación lógica

Una aplicación lógica consta de tres componentes básicos:

* **Recursos de aplicación lógica**: contiene información acerca de aspectos como definición de flujo de trabajo de hello, la ubicación y el plan de precios.
* **Definición de flujo de trabajo**: describe los pasos de flujo de trabajo de la aplicación lógica y cómo motor de Logic Apps Hola debe ejecutar el flujo de trabajo de Hola.
Puede ver esta definición en la ventana **Vista código** de su aplicación lógica.
En el recurso de aplicación lógica de hello, puede encontrar esta definición en hello `definition` propiedad.
* **Las conexiones**: hace referencia a los recursos de tooseparate que almacenan metadatos acerca de las conexiones de conector, como una cadena de conexión y un token de acceso de forma segura.
En el recurso de aplicación lógica de hello, la aplicación lógica hace referencia a estos recursos en hello `parameters` sección.

Puede ver todas estas piezas de las aplicaciones lógicas existentes mediante herramientas como el [Explorador de recursos de Azure](http://resources.azure.com).

toomake una plantilla para una aplicación de lógica toouse con implementaciones de grupos de recursos, debe definir recursos de Hola y parametrizar según sea necesario.
Por ejemplo, si va a implementar tooa desarrollo, prueba y entorno de producción, probablemente desee toouse otra conexión cadenas tooa base de datos SQL en cada entorno.
O bien, puede querer toodeploy en distintas suscripciones o grupos de recursos.  

## <a name="create-a-logic-app-deployment-template"></a>Creación de una plantilla de implementación de aplicación lógica

toohave de manera más fácil de Hello una plantilla de implementación de aplicación lógica válida es toouse el [Visual Studio Tools para aplicaciones lógicas](logic-apps-deploy-from-vs.md).
herramientas de Visual Studio de Hello generar una plantilla de implementación válido que puede utilizarse en cualquier suscripción o la ubicación.

Algunas herramientas pueden ayudarle a crear una plantilla de implementación de aplicación lógica.
Puede crear manualmente, es decir, mediante el uso de hello recursos ya tratan aquí toocreate parámetros según sea necesario.
Otra opción es toouse una [creador de plantillas de aplicación lógica](https://github.com/jeffhollan/LogicAppTemplateCreator) módulo de PowerShell. Este módulo de código abierto evalúa primero la aplicación de la lógica de hello y que las conexiones que está usando y, a continuación, genera los recursos de plantilla con los parámetros necesarios para la implementación de Hola.
Por ejemplo, si tiene una aplicación de lógica que recibe un mensaje de una cola de Service Bus de Azure y agrega la base de datos de SQL Azure de datos tooan, herramienta de hello conserva toda lógica de orquestación de Hola y parametriza Hola SQL y cadenas de conexión de Bus de servicio para que se pueden establecer en la implementación.

> [!NOTE]
> Las conexiones deben ser dentro de hello mismo grupo de recursos como aplicación de lógica de hello.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Instalar el módulo de PowerShell de plantilla de aplicación de lógica de Hola
módulo de Hola de manera más fácil de Hello tooinstall es a través de hello [Galería de PowerShell](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), mediante el comando de hello `Install-Module -Name LogicAppTemplate`.  

También puede instalar módulo de PowerShell de hello manualmente:

1. Descargar la versión más reciente de Hola de hello [creador de plantillas de aplicación lógica](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. Extraer la carpeta de hello en la carpeta del módulo de PowerShell (normalmente `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Para hello módulo toowork con cualquier acceso inquilino y suscripción símbolo (token), se recomienda utilizarlo con hello [ARMClient](https://github.com/projectkudu/ARMClient) herramienta de línea de comandos.  Esta [entrada de blog ](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) describe ARMClient con más detalle.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>Generación de una plantilla de aplicación lógica mediante PowerShell
Después de instala PowerShell, puede generar una plantilla mediante Hola siguiente comando:

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`es el Id. de suscripción de Azure Hola. Esta línea recibe primero un acceso token a través de ARMClient, a continuación, canaliza a través de toohello secuencia de comandos de PowerShell y, a continuación, crea la plantilla de hello en un archivo JSON.

## <a name="add-parameters-tooa-logic-app-template"></a>Agregar plantilla de aplicación lógica de parámetros tooa
Después de crear la plantilla de aplicación lógica, puede continuar tooadd o modificar los parámetros que necesite. Por ejemplo, si la definición incluye un Id. de recurso tooan función Azure o flujo de trabajo anidado tiene previsto toodeploy en una sola implementación, puede agregar más recursos tooyour plantilla y parametrizar identificadores según sea necesario. Hello Esto mismo aplica tooany referencias toocustom API Swagger extremos o esperar toodeploy de cada grupo de recursos.

## <a name="deploy-a-logic-app-template"></a>Implementación de una plantilla de aplicación lógica

Puede implementar la plantilla mediante cualquier herramienta como PowerShell, API de REST, [Visual Studio Team Services Release Management](#team-services)y la implementación de plantilla a través de hello portal de Azure.
Además, valores de hello toostore para los parámetros, le recomendamos que cree una [archivo de parámetros](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Obtenga información acerca de cómo demasiado[implementar los recursos con plantillas del Administrador de recursos de Azure y PowerShell](../azure-resource-manager/resource-group-template-deploy.md) o [implementar los recursos con plantillas del Administrador de recursos de Azure y Hola portal de Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>Autorización de conexiones de OAuth

Después de la implementación, aplicación de lógica de hello funciona to-end con parámetros válidos.
Sin embargo, todavía debe autorizar conexiones de OAuth toogenerate un token de acceso válido.
tooauthorize OAuth conexiones, abra la aplicación de lógica de Hola Hola Diseñador de aplicaciones de la lógica y autorizar estas conexiones. O bien, para la implementación automatizada, puede usar un tooeach de tooconsent OAuth conexión de script.
Hay un script de ejemplo en GitHub, en el proyecto [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) .

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Administración de versiones de Visual Studio Team Services

Un escenario común para implementar y administrar un entorno es toouse una herramienta como la administración de versiones en Visual Studio Team Services, con una plantilla de implementación de aplicación lógica. Visual Studio Team Services incluye un [implementar un grupo de recursos de Azure](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) tareas que puede agregar tooany compilación o la versión de canalización. Necesita toohave una [entidad de servicio](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) para la autorización toodeploy y, a continuación, puede generar definición de la versión de Hola.

1. En Release Management, seleccione **Vacío** para crear una definición vacía.

    ![Creación de una definición vacía][1]

2. Elija el proceso de compilación de todos los recursos que necesita para esta, probablemente incluido Hola lógica plantilla de aplicación que se genera manualmente o como parte del programa Hola.
3. Agregue una tarea de **Implementación de un grupo de recursos de Azure** .
4. Configurar con un [entidad de servicio](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)y hacer referencia a los archivos de plantilla y parámetros de plantilla de Hola.
5. Continuar toobuild pasos en el proceso de lanzamiento de Hola para cualquier otro entorno, pruebas automatizadas o aprobadores según sea necesario.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
