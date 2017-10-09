---
title: "una aplicación en Visual Studio sin servidor aaaBuild | Documentos de Microsoft"
description: "Introducción a la primera aplicación sin servidor con esta guía sobre cómo crear, implementar y administrar la aplicación hello en Visual Studio."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Cree una aplicación sin servidor en Visual Studio con Logic Apps y Functions

Las herramientas y funcionalidades sin servidor de Azure permiten desarrollar e implementar aplicaciones rápidamente en la nube.  Este documento se centra en cómo tooget inició en Visual Studio compilar una aplicación sin servidor.  Encontrará información general sobre soluciones sin servidor en [este artículo](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>Preparación

Estos es una aplicación desde Visual Studio sin servidor hello toobuild de requisitos previos necesarios:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) o Visual Studio 2015 - Community, Professional o Enterprise
* [Herramientas de Logic Apps para Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [SDK de Azure más reciente](https://azure.microsoft.com/downloads/) (2.9.1 o superior)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Herramientas de Azure funciones principales](https://www.npmjs.com/package/azure-functions-core-tools) toodebug funciona localmente
* Web toohello de acceso al usar Hola incrustado Diseñador de aplicación lógica

## <a name="getting-started-with-a-deployment-template"></a>Introducción a las plantillas de implementación

La administración de recursos en Azure se realiza en un grupo de recursos.  Un grupo de recursos es una agrupación lógica de recursos.  Los grupos de recursos permiten la implementación y administración de una colección de recursos.  Para una aplicación sin servidor de Azure, nuestro grupo de recursos contiene Azure Logic Apps y Azure Functions.  Mediante el uso de proyecto del grupo de recursos de hello en Visual Studio, estamos toodevelop capaz de, administrar e implementar toda aplicación de Hola como un solo activo.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Creación de un proyecto de grupo de recursos en Visual Studio

1. En Visual Studio, haga clic en tooadd un **nuevo proyecto**
1. Hola **nube** categoría, seleccione toocreate un Azure **grupo de recursos** proyecto  
 * Si no ve la categoría de Hola o proyecto en la lista, asegúrese de que dispone de hello Azure SDK de Visual Studio instalada
1. Asigne el proyecto de hello un nombre y una ubicación y seleccione **Aceptar** toocreate Visual Studio le pide tooselect una plantilla.  Puede seleccionar toostart de espacio en blanco, empiece con una lógica de aplicación u otro recurso.  Sin embargo, en este caso usamos una tooget de plantilla de inicio rápido de Azure que nos a trabajar con una aplicación sin servidor.
1. Seleccionar plantillas de tooshow de **inicio rápido de Azure** ![plantillas de selección de inicio rápido de Azure][1]
1. Plantilla de inicio rápido sin servidor seleccione hello: **101-logic-app-and-function-app** y haga clic en **Aceptar**

plantilla de inicio rápido de Hello crea una plantilla de implementación en el proyecto del grupo de recursos.  plantilla de Hello contiene una aplicación sencilla de lógica que llama a una función de Azure y devuelve el resultado de hello.  Si abre hello `azuredeploy.json` Hola de archivo en el Explorador de soluciones, puede ver recursos de hello para la aplicación sin servidor hello.

## <a name="deploying-hello-serverless-application"></a>Implementación de aplicación sin servidor hello

Para poder abrir el diseñador visual de aplicación lógica de hello en Visual Studio, es necesario toobe un grupo de recursos de Azure implementado previamente.  Esto permite toocreate diseñador hello y tooresources de las conexiones de uso y los servicios de aplicación lógica de hello.  tooget iniciado, simplemente necesitamos toodeploy Hola solución creado.

1. Menú contextual proyecto de hello en Visual Studio, seleccione **implementar**y crear un **New** implementación ![seleccionando la nueva implementación de recursos][2]
1. Seleccione una suscripción válida a Azure y el grupo de recursos
1. Seleccione también**implementar** Hola solución
1. Escriba en nombre de hello para la aplicación lógica de Hola y Hola función aplicación de Azure.  nombre de la función de Azure de Hello necesita toobe único global

solución sin servidor Hello se implementa en el grupo de recursos especificado de Hola.  Si observa hello **salida** en Visual Studio puede ver el estado de Hola de implementación de Hola.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Editar aplicación de lógica de hello en Visual Studio

Una vez que se haya implementado la solución de Hola en cualquier grupo de recursos, diseñador visual de Hola puede ser usado tooedit y realizar cambios toohello lógica aplicación.

1. Hola contextual `azuredeploy.json` un archivo en el Explorador de soluciones de Hola y seleccione **abrir con lógica de aplicaciones de diseñador**
1. Seleccione hello **grupo de recursos** y **ubicación** ha venido siendo Hola implementado tooand seleccione **Aceptar**

diseñador visual de aplicación lógica de Hello ahora debe ser visible con Visual Studio.  Puede seguir pasos tooadd, modifique el flujo de trabajo de Hola y guardar los cambios.  También puede crear aplicaciones lógicas desde Visual Studio.  Si hace doble clic en hello **recursos** en el Explorador de la plantilla de hello, puede elegir tooadd una **aplicación lógica** toohello proyecto.  Cargar aplicaciones lógicas vacío en el diseñador visual de hello sin un implementar previamente en un grupo de recursos.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Administración y visualización del historial de ejecución de una aplicación de la lógica implementada

También puede administrar y ver el historial de hello ejecutar para logic apps implementado en Azure.  Si abre hello **Explorer nube** herramienta en Visual Studio, puede haga clic en cualquier aplicación lógica y elija tooedit, deshabilitar, ver las propiedades o ver el historial de ejecución.  Haga clic en Editar también le permite toodownload una aplicación publicada lógica en un proyecto del grupo de recursos de Visual Studio.  Esto significa que aunque empezó a crear la aplicación lógica en hello portal de Azure, puede seguir importarlo y administrarla desde Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Desarrollo de una función de Azure en Visual Studio

plantilla de implementación Hello implementa las funciones de Azure que se encuentran en la solución de hello para el repositorio de git Hola especificado en hello `azuredeploy.json` variables.  Si creas un proyecto de función dentro de la solución de Hola, protegerlo en el control de código fuente (GitHub, Visual Studio Team Services, etc.) y actualizar hello `repo` variable, plantilla de hello implementará Hola función de Azure.

### <a name="creating-an-azure-function-project"></a>Creación de una función de Azure

Si usa JavaScript, Python, F #, intensiva de errores, lote o PowerShell, siga hello [los pasos de hello funciones CLI](../azure-functions/functions-run-local.md) toocreate un proyecto.  Si desarrolla una función en C#, puede usar un [biblioteca de clases de C#](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) en la solución actual de Hola Hola función de Azure.

## <a name="next-steps"></a>Pasos siguientes

* [Obtenga información acerca de cómo toobuild un panel sociales sin servidor](logic-apps-scenario-social-serverless.md)
* [Administrar una aplicación lógica desde Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Lenguaje de definición de flujo de trabajo en una aplicación lógica](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
