---
title: "aplicaciones de la lógica de aaaManage en Visual Studio: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Administración de aplicaciones lógicas y otros recursos de Azure con Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Administración de sus aplicaciones lógicas con Visual Studio Cloud Explorer

Aunque hello [portal de Azure](https://portal.azure.com/) ofrece una excelente manera de que toodesign y administrar las aplicaciones lógicas de Azure, puede usar el Explorador de Visual Studio en la nube para administrar muchos de los activos de Azure, incluidas las aplicaciones de lógica. Visual Studio Cloud Explorer le permite explorar, administrar, editar y descargar aplicaciones lógicas publicadas. Las tareas de administración incluyen habilitar, deshabilitar y ver el historial de ejecuciones. 

Para poder acceder a las aplicaciones lógicas y administrarlas en Visual Studio, instale y configure estas herramientas de Visual Studio para Azure Logic Apps. 

## <a name="prerequisites"></a>Requisitos previos

* [Visual Studio 2015 o Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [SDK de Azure más reciente](https://azure.microsoft.com/downloads/) (2.9.1 o superior)
* [Visual Studio Cloud Explorer](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* Web toohello de acceso al usar el Diseñador de hello incrustado

## <a name="install-visual-studio-tools-for-logic-apps"></a>Instalación de herramientas de Visual Studio para Logic Apps

Después de instalar requisitos previos de hello, descargar e instalar aplicaciones de lógica de hello Azure Tools para Visual Studio.

1. Abra Visual Studio. En hello **herramientas** menú, seleccione **extensiones y actualizaciones**.
2. Expanda hello **Online** categoría para que puedan buscar en línea en hello Galería de Visual Studio.
3. Busque **Logic Apps** hasta que encuentre las **herramientas de Azure Logic Apps para Visual Studio**.
4. toodownload y la extensión de Hola de instalación, haga clic en **descargar**.
5. Reinicie Visual Studio después de la instalación.

> [!NOTE]
> Hola toodownload aplicaciones de lógica de Azure Tools para Visual Studio ir directamente, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Búsqueda de aplicaciones lógicas en Cloud Explorer

1.  tooopen el explorador en la nube, en hello **vista** menú, elija **nube explorador**.
2.  Busque la aplicación lógica. Puede hacerlo por grupo de recursos o por tipo de recurso. 

    * Si se desplaza por tipo de recurso, seleccione la suscripción de Azure, expanda hello **Logic Apps** sección y seleccionar la aplicación lógica. 
    * Si se desplaza por grupo de recursos, expanda grupo de recursos de Hola que tiene la aplicación lógica y seleccione la aplicación lógica.

    tooview comandos para la aplicación lógica, haga clic en la aplicación lógica, o final Hola de explorador en la nube, elija de hello **acciones** menú.

    ![Búsqueda de su aplicación lógica](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Edición de la aplicación lógica con el Diseñador de Logic Apps

Desde el Explorador de la nube, puede abrir una aplicación de la lógica implementada actualmente en hello mismo diseñador que se utiliza en hello portal de Azure. 

* tooedit la lógica de aplicación, en el explorador en la nube, haga clic en la aplicación lógica y seleccione **abierto con el Editor de aplicación lógica**. 

* toopublish su toohello actualizaciones en la nube, elija **publicar**. 

* toostart una nueva ejecución, elija **desencadenador ejecutar**.

![Diseñador de Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

Desde el Diseñador de hello, también puede **descargar** una aplicación lógica. Esta acción automáticamente parametriza la definición de aplicación lógica de Hola y guarda la definición de hello como una plantilla de implementación de Azure Resource Manager. Puede agregar este proyecto de grupo de recursos de Azure de tooyour de plantilla de implementación.

## <a name="browse-your-logic-app-run-history"></a>Búsqueda del historial de ejecución de su aplicación lógica

Hola tooview historial para la aplicación de la lógica de ejecución haga clic en la aplicación lógica y seleccione **historial de ejecución de abrir**. tooreorder su historial de ejecución se basa en cualquier encabezado de columna de Hola se muestra, seleccione Propiedades de Hola.

![Historial de ejecuciones](media/logic-apps-manage-from-vs/runs.png)

Hola tooshow historial de una instancia de ejecución para poder revisar Hola ejecutar resultados, incluidas Hola entradas y salidas de cada paso, haga doble clic en uno de hello ejecutar instancias.

![Resultados del historial de ejecuciones, entradas y salidas de los pasos](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Pasos siguientes

* [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](logic-apps-create-a-logic-app.md)
* [Creación e implementación de aplicaciones lógicas en Visual Studio](logic-apps-deploy-from-vs.md)
* [Ejemplos de aplicaciones lógicas y escenarios comunes](logic-apps-examples-and-scenarios.md)
* [Vídeo: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (Automatización de los procesos de negocio con Azure Logic Apps)
* [Vídeo: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (Integración de los sistemas con Azure Logic Apps)
