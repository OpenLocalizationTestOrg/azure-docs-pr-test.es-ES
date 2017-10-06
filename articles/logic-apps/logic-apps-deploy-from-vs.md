---
title: "aaaCreate, genere e implemente las aplicaciones lógicas en Visual Studio: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Cree proyectos de Visual Studio para diseñar, compilar e implementar Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Diseño, compilación e implementación de Azure Logic Apps en Visual Studio

Aunque hello [portal de Azure](https://portal.azure.com/) ofrece una excelente manera de que toocreate y administrar las aplicaciones lógicas de Azure, puede usar Visual Studio para diseñar, crear e implementar las aplicaciones lógicas. Visual Studio proporciona herramientas enriquecidos como Hola diseñador la lógica de aplicación para toocreate las aplicaciones lógicas, configurar las plantillas de implementación y automatización e implementar tooany entorno. 

Obtenga información acerca de tooget a trabajar con las aplicaciones lógicas de Azure, [cómo toocreate su primera aplicación de lógica en el portal de Azure hello](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Pasos de instalación

tooinstall y configurar las herramientas de Visual Studio para aplicaciones de la lógica de Azure, siga estos pasos.

### <a name="prerequisites"></a>Requisitos previos

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) o Visual Studio 2015
* [SDK de Azure más reciente](https://azure.microsoft.com/downloads/) (2.9.1 o superior)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* Web toohello de acceso al usar el Diseñador de hello incrustado

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Instalación de herramientas de Visual Studio para Azure Logic Apps

Después de instalar requisitos previos de hello:

1. Abra Visual Studio. En hello **herramientas** menú, seleccione **extensiones y actualizaciones**.
2. Expanda hello **Online** categoría de forma que pueda buscar en línea.
3. Busque **Logic Apps** hasta que encuentre las **herramientas de Azure Logic Apps para Visual Studio**.
4. toodownload y la extensión de Hola de instalación, haga clic en **descargar**.
5. Reinicie Visual Studio después de la instalación.

> [!NOTE]
> También puede descargar [aplicaciones de lógica de Azure Tools para Visual Studio de 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) hello y [aplicaciones de lógica de Azure Tools para Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directamente desde Visual Studio Marketplace Hola.

Después de finalizar la instalación, puede usar el proyecto del grupo de recursos de Azure de Hola con lógica de aplicación diseñador.

## <a name="create-your-project"></a>Creación del proyecto

1. En hello **archivo** menú, ir demasiado**New**y seleccione **proyecto**. O tooadd su tooan proyecto existente de solución, vaya demasiado**agregar**y seleccione **nuevo proyecto**.

    ![Menú Archivo](./media/logic-apps-deploy-from-vs/filemenu.png)

2. Hola **nuevo proyecto** ventana, buscar **nube**y seleccione **grupo de recursos de Azure**. Asigne un nombre al proyecto y haga clic en **Aceptar**.

    ![Incorporación de proyecto nuevo](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Seleccione hello **aplicación lógica** plantilla, que crea una plantilla de implementación de aplicación lógica en blanco de toouse. Cuando la haya seleccionado, haga clic en **Aceptar**.

    ![Selección de la plantilla de aplicación lógica](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    Ahora ha agregado la solución de tooyour de proyecto de aplicación lógica. 
    En el Explorador de soluciones de hello, debe aparecer el archivo de implementación.

    ![Archivo de implementación](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Creación de la aplicación lógica en Diseñador de aplicación lógica

Cuando tenga un proyecto del grupo de recursos de Azure que contiene una aplicación de lógica, puede abrir Hola diseñador la lógica de aplicación en Visual Studio toocreate el flujo de trabajo. 

> [!NOTE]
> Diseñador de Hello requiere una conexión a internet demasiado consultar conectores de datos y propiedades disponibles. Por ejemplo, si usa el conector de Dynamics CRM Online hello, Diseñador de hello consulta su personalizado disponible de CRM instancia tooshow y propiedades predeterminadas.

1. Haga clic con el botón derecho en el archivo `<template>.json` y seleccione **Open with Logic App Designer** (Abrir con diseñador de aplicación lógica). (`Ctrl+L`)

2. Elija la suscripción de Azure, el grupo de recursos y la ubicación para la plantilla de implementación.

    > [!NOTE]
    > El diseño de una aplicación lógica creará recursos de una conexión de API para consultar las propiedades durante el diseño. Visual Studio usa el toocreate del grupo de recursos seleccionado esas conexiones en tiempo de diseño. tooview o cambiar las conexiones de API, vaya toohello portal de Azure y busque **API conexiones**.

    ![Selector de suscripción](./media/logic-apps-deploy-from-vs/designer_picker.png)

    Diseñador de Hello utiliza la definición de Hola Hola `<template>.json` archivo para la representación.

4. Cree y diseñe la aplicación lógica. La plantilla de implementación se actualiza con los cambios.

    ![Diseñador de aplicaciones lógicas en Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio agrega `Microsoft.Web/connections` recursos demasiado el archivo de recursos para las conexiones toofunction necesita de la aplicación de lógica. Estas propiedades de conexión se pueden establecer cuando se implementa y administra después de implementar en **API conexiones** Hola portal de Azure.

### <a name="switch-toojson-code-view"></a>Cambiar la vista de código tooJSON

Hola tooshow representación JSON de la aplicación lógica, seleccione hello **en la vista código** pestaña final Hola de diseñador Hola.

tooswitch atrás toohello completa a recursos JSON, haga clic en hello `<template>.json` de archivos y seleccione **abiertos**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Agregar referencias para plantillas de implementación de los recursos dependientes tooVisual Studio

Si desea que los recursos dependientes de la tooreference de aplicación lógica, puede usar [funciones de plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) en la plantilla de implementación de aplicación lógica. Por ejemplo, puede que su tooreference de aplicación lógica una cuenta de integración o de función de Azure que desea que toodeploy junto con la aplicación lógica. Siga estas instrucciones sobre cómo se representa correctamente toouse parámetros en la plantilla de implementación para Hola diseñador la lógica de aplicación. 

Puede usar parámetros de aplicación lógica en estos tipos de desencadenadores y acciones:

*   Flujo de trabajo secundario
*   Aplicación de función
*   Llamada APIM
*   Dirección URL en tiempo de ejecución de conexión de API
*   Ruta de conexión de API

Y puede utilizar funciones de plantilla como, por ejemplo, parámetros, variables, resourceId, concat, etc. Por ejemplo, mostramos cómo puede reemplazar el Id. de recurso de Azure función hello:

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

Y dónde usaría parámetros:

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
Otro ejemplo puede parametrizar Hola operación de mensaje de envío de Bus de servicio:

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl es opcional y se puede quitar de la plantilla si está presente.
> 


> [!NOTE] 
> Para toowork del Diseñador de la aplicación lógica de Hola para utilizar parámetros, debe proporcionar valores predeterminados, por ejemplo:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Guardado de la aplicación lógica

toosave la aplicación lógica y en cualquier momento, vaya demasiado**archivo** > **guardar**. (`Ctrl+S`) 

Si la aplicación lógica tiene errores cuando guarda la aplicación, que aparecen en Visual Studio hello **salidas** ventana.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Implementación de la aplicación lógica desde Visual Studio

Después de configurar la aplicación, puede realizar la implementación directamente desde Visual Studio en solo un par de pasos. 

1. En el Explorador de soluciones, haga clic en el proyecto y vaya demasiado**implementar** > **nueva implementación...**

    ![Nueva implementación](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. Cuando se le pida, inicie sesión en tooyour suscripción de Azure. 

3. Ahora debe seleccionar detalles de Hola Hola para grupo de recursos donde desea toodeploy la aplicación lógica. Cuando haya terminado, haga clic en **Implementar**.

    > [!NOTE]
    > Asegúrese de que selecciona plantilla correcta de Hola y el archivo de parámetros para el grupo de recursos de Hola. Por ejemplo, si desea que el entorno de producción de toodeploy tooa, elija el archivo de parámetros de producción de hello.

    ![Implementar grupo tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    estado de la implementación de Hello aparece en hello **salida** ventana. 
    Es posible que tenga tooselect **Azure aprovisionamiento** en hello **mostrar resultados desde** lista.

    ![Salida del estado de la implementación](./media/logic-apps-deploy-from-vs/output.png)

Hola futuro, puede editar la aplicación lógica de control de código fuente y usa toodeploy nuevas versiones de Visual Studio.

> [!NOTE]
> Si cambia la definición de Hola Hola portal de Azure directamente, los cambios se sobrescriben cuando se implementa desde Visual Studio próxima vez. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Agregar el proyecto existente de grupo de recursos de la lógica aplicación tooan

Si tiene un proyecto del grupo de recursos existente, puede agregar el proyecto de toothat de aplicación lógica en la ventana de esquema de JSON de Hola. También puede agregar otra lógica de aplicación, junto con la aplicación hello que creó anteriormente.

1. Abra hello `<template>.json` archivo.

2. Hola tooopen ventana Esquema de JSON, vaya demasiado**vista** > **otras ventanas** > **esquema JSON**.

3. Haga clic en un archivo de plantilla de recursos toohello, tooadd **Agregar recurso** en parte superior de Hola de ventana de esquema de JSON de Hola. O en la ventana de esquema de JSON de hello, haga clic en **recursos**y seleccione **Agregar nuevo recurso**.

    ![Ventana Esquema JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. Hola **Agregar recurso** cuadro de diálogo, busque y seleccione **aplicación lógica**. Asigne un nombre a la aplicación lógica y elija **Agregar**.

    ![Agregar recurso](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Pasos siguientes

* [Administración de aplicaciones lógicas con Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Ejemplos de aplicaciones lógicas y escenarios comunes](logic-apps-examples-and-scenarios.md)
* [Obtenga información acerca de cómo los procesos del negocio tooautomate con las aplicaciones lógicas de Azure](http://channel9.msdn.com/Events/Build/2016/T694)
* [Obtenga información acerca de cómo toointegrate los sistemas con las aplicaciones lógicas de Azure](http://channel9.msdn.com/Events/Build/2016/P462)
