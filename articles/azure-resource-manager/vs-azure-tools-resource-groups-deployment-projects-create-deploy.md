---
title: proyectos de grupo de recursos de Azure en Studio aaaVisual | Documentos de Microsoft
description: Usar Visual Studio toocreate un proyecto del grupo de recursos de Azure e implementar Hola recursos tooAzure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Creación e implementación de grupos de recursos de Azure mediante Visual Studio
Con Visual Studio y hello [Azure SDK](https://azure.microsoft.com/downloads/), puede crear un proyecto que implementa su tooAzure de infraestructura y el código. Por ejemplo, puede definir el host de web hello, sitio web y base de datos para la aplicación e implementar esa infraestructura junto con el código de hello. O bien, puede definir una máquina virtual, una red virtual y una cuenta de almacenamiento e implementar esa infraestructura junto con un script que se ejecuta en la máquina virtual. Hola **grupo de recursos de Azure** proyecto de implementación permite toodeploy todos los recursos de hello necesitado en una única operación repetible. Para más información sobre la implementación y administración de recursos, consulte [Información general de Azure Resource Manager](resource-group-overview.md).

Proyectos de grupo de recursos de Azure contienen plantillas de Azure Resource Manager JSON, que definen los recursos de Hola que implemente tooAzure. toolearn acerca de los elementos de Hola de plantilla del Administrador de recursos de hello, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md). Visual Studio permite tooedit estas plantillas y proporciona herramientas que simplifican el trabajo con plantillas.

En este artículo se implementa una aplicación web y SQL Database. Sin embargo, los pasos de Hola se casi Hola mismo para cualquier recurso de tipo. Puede implementar fácilmente una máquina virtual y sus recursos relacionados. Visual Studio proporciona muchas plantillas de inicio diferentes para la implementación de escenarios comunes.

Este artículo muestra Visual Studio 2017. Si usa Visual Studio 2015 Update 2 y Microsoft Azure SDK para .NET 2.9 o Visual Studio 2013 con Azure SDK 2.9, su experiencia es en gran medida Hola igual. Puede usar las versiones de hello Azure SDK desde 2.6 o posterior; Sin embargo, la experiencia de interfaz de usuario de hello puede ser diferente de interfaz de usuario de hello mostrado en este artículo. Se recomienda encarecidamente que instale la versión más reciente de Hola de hello [Azure SDK](https://azure.microsoft.com/downloads/) antes de iniciar los pasos de Hola. 

## <a name="create-azure-resource-group-project"></a>Creación de un proyecto de grupo de recursos de Azure
En este procedimiento, va a crear un proyecto de grupo de recursos de Azure con la plantilla **Aplicación web + SQL** .

1. En Visual Studio, elija **Archivo**, **Nuevo proyecto** y **C#** o **Visual Basic**. Luego, elija **Nube** y el proyecto **Grupo de recursos de Azure**.
   
    ![Proyecto de implementación de la nube](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Elija la plantilla de Hola que desea toodeploy tooAzure el Administrador de recursos. Observe que hay muchas opciones diferentes en función de hello tipo de proyecto que desea toodeploy. En este artículo, elija hello **Web app + SQL** plantilla.
   
    ![Seleccionar una plantilla](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    plantilla de Hola que se puede seleccionar es simplemente un punto de partida; Puede agregar y quitar recursos toofulfill su escenario.
   
   > [!NOTE]
   > Visual Studio recupera una lista de las plantillas disponibles en línea. puede cambiar la lista de Hola.
   > 
   > 
   
    Visual Studio crea un proyecto de implementación de grupo de recursos para la aplicación web de hello y base de datos SQL.
3. toosee lo que ha creado, busque en el nodo de hello en el proyecto de implementación de Hola.
   
    ![mostrar nodos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Dado que elegimos la aplicación Web de hello + plantilla SQL para este ejemplo, vea Hola siguientes archivos: 
   
   | Nombre de archivo | Description |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Un script de PowerShell que invoca PowerShell comandos toodeploy tooAzure el Administrador de recursos.<br />**Tenga en cuenta** Visual Studio usa este toodeploy de secuencia de comandos de PowerShell de la plantilla. Los cambios que realice la secuencia de comandos de toothis afecta a la implementación en Visual Studio, por lo que debe tener cuidado. |
   | WebSiteSQLDatabase.json |plantilla de administrador de recursos de Hola que define la infraestructura de Hola que desee implementar tooAzure y los parámetros de hello que puede proporcionar durante la implementación. También define las dependencias de hello entre recursos de hello para que el Administrador de recursos implementa los recursos de hello en el orden correcto de Hola. |
   | WebSiteSQLDatabase.parameters.json |Un archivo de parámetros que contiene los valores requeridos por la plantilla de Hola. Se pasa en toocustomize de valores de parámetro de cada implementación. |
   
    Todos los proyectos de implementación del grupo de recursos contienen estos archivos básicos. Otros proyectos pueden contener archivos adicionales toosupport otras funcionalidades.

## <a name="customize-hello-resource-manager-template"></a>Personalizar la plantilla de administrador de recursos de Hola
Puede personalizar un proyecto de implementación mediante la modificación de plantillas JSON de Hola que se describen los recursos de Hola que desee toodeploy. JSON significa JavaScript Object Notation y es un formato de datos serializados que es fácil toowork con. archivos de Hello JSON usan un esquema que se hace referencia en parte superior de Hola de cada archivo. Si se desea toounderstand Hola esquema, puede descargar y analizarlo. Hello esquema define qué elementos son válidos, hello tipos y formatos de campos, Hola valores posibles de los valores enumerados y así sucesivamente. toolearn acerca de los elementos de Hola de plantilla del Administrador de recursos de hello, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).

Abra toowork en la plantilla, **WebSiteSQLDatabase.json**.

Hola Visual Studio, el editor proporciona herramientas tooassist que con la edición de Hola plantilla del Administrador de recursos. Hola **esquema JSON** ventana facilita elementos de hello toosee fácil definidos en la plantilla.

![mostrar el esquema JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Si se selecciona cualquiera de los elementos de hello en el esquema de Hola toma toothat parte de la plantilla de Hola y resalta Hola correspondiente JSON.

![navegar a JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

Puede agregar un recurso por cualquier selección hello **Agregar recurso** situado en la parte superior de la ventana de esquema de JSON de hello, o con el botón secundario de hello **recursos** y seleccionando **Agregar nuevo recurso**.

![agregar recurso](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Para este tutorial, seleccione **Cuenta de almacenamiento** y asígnele un nombre. Proporcione un nombre que no tenga más de 11 caracteres y que solo contenga números y letras minúsculas.

![agregar almacenamiento](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Tenga en cuenta que no solo se agregó el recurso de hello, sino también un parámetro para hello escriba cuenta de almacenamiento y una variable para hello nombre de cuenta de almacenamiento de Hola.

![mostrar el esquema](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Hola **storageType** parámetro está predefinido con los tipos permitidos y un tipo predeterminado. Puede dejar estos valores o modificarlos para su escenario específico. Si no quiere que nadie toodeploy una **Premium_LRS** cuenta de almacenamiento a través de esta plantilla, quitarlo de hello tipos permitido. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio también proporciona toohelp intellisense comprender qué propiedades están disponibles al editar plantilla Hola. Por ejemplo, propiedades de hello tooedit para el plan de servicio de aplicaciones, desplácese toohello **HostingPlan** recursos y agregue un valor para hello **propiedades**. Tenga en cuenta que intellisense muestra los valores disponibles de Hola y proporciona una descripción de ese valor.

![mostrar IntelliSense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

Puede establecer **numberOfWorkers** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Implementar tooAzure de proyecto del grupo de recursos de Hola
Se está ahora listo toodeploy el proyecto. Al implementar un proyecto del grupo de recursos de Azure, se implementa tooan grupo de recursos de Azure. grupo de recursos de Hello es una agrupación lógica de recursos que comparten un ciclo de vida comunes.

1. En el menú contextual de hello del nodo de proyecto de implementación de hello, elija **implementar** > **nuevo**.
   
    ![Implementar, elemento de menú Nueva implementación](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Hola **implementar tooResource grupo** aparece el cuadro de diálogo.
   
    ![Implementar tooResource cuadro de diálogo de grupo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. Hola **grupo de recursos** cuadro de lista desplegable, elija un grupo de recursos existente o cree uno nuevo. toocreate un grupo de recursos, abra hello **grupo de recursos** lista desplegable y elija **crear nuevo**.
   
    ![Implementar tooResource cuadro de diálogo de grupo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Hola **crear grupo de recursos** aparece el cuadro de diálogo. Asigne el grupo de un nombre y ubicación y seleccione hello **crear** botón.
   
    ![Cuadro de diálogo Crear grupo de recursos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Editar parámetros de hello para la implementación de hello seleccionando hello **editar parámetros** botón.
   
    ![Botón Editar parámetros](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Proporcionar valores para parámetros vacía hello y seleccione hello **guardar** botón. Hola vacía parámetros son **hostingPlanName**, **Iniciodesesióndeadministrador**, **administratorLoginPassword**, y **databaseName**.
   
    **hostingPlanName** especifica un nombre para hello [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **Iniciodesesióndeadministrador** especifica el nombre de usuario de hello para el Administrador de SQL Server de Hola. No utilice nombres de administrador comunes como **sa** o **admin**. 
   
    Hola **administratorLoginPassword** especifica una contraseña de administrador de SQL Server. Hola **guardar las contraseñas como texto sin formato en el archivo de parámetros de hello** opción no está seguro; por lo tanto, no seleccione esta opción. Dado que no se guarda la contraseña de hello como texto sin formato, debe tooprovide esta contraseña durante la implementación. 
   
    **databaseName** especifica un nombre para hello toocreate de base de datos. 
   
    ![Cuadro de diálogo Editar parámetros](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Elija hello **implementar** botón toodeploy Hola proyecto tooAzure. Se abre una consola de PowerShell fuera de la instancia de Visual Studio Hola. Escriba la contraseña de administrador de SQL Server de hello en la consola de PowerShell de hello cuando se le solicite. **La consola de PowerShell podría estar oculta detrás de otros elementos o minimizada en la barra de tareas de Hola.** Busque esta consola y seleccione contraseña de hello tooprovide.
   
   > [!NOTE]
   > Visual Studio puede pedirle que tooinstall Hola cmdlets de PowerShell de Azure. Necesita hello Azure PowerShell cmdlets toosuccessfully implementar grupos de recursos. Si se le solicita, instálelos.
   > 
   > 
6. implementación de Hello puede tardar unos minutos. Hola **salida** windows, vea Hola estado de implementación de Hola. Cuando haya terminado la implementación de hello, último mensaje de Hola indica una implementación correcta con algo parecido a:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. En un explorador, abra hello [portal de Azure](https://portal.azure.com/) e inicie sesión en la cuenta de tooyour. grupo de recursos de hello toosee, seleccione **grupos de recursos** y que se implementan en el grupo de recursos de Hola.
   
    ![seleccionar grupo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Vea todos los recursos de hello implementado. Tenga en cuenta ese nombre Hola de Hola cuenta de almacenamiento no es exactamente lo que se especifica al agregar ese recurso. cuenta de almacenamiento de Hello debe ser único. Hello plantilla agrega automáticamente una cadena de nombre de toohello de caracteres proporcionado tooprovide un nombre único. 
   
    ![mostrar recursos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Si realiza cambios y desea tooredeploy el proyecto, elija el grupo de recursos existente de hello en menú contextual de Hola de proyecto del grupo de recursos de Azure. En el menú contextual de hello, elija **implementar**y, a continuación, elija grupo de recursos de hello ha implementado.
   
    ![Grupo de recursos de Azure implementado](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Implementación de código con la infraestructura
En este momento, ha implementado una infraestructura hello para la aplicación, pero no hay ningún código real que se implementa con el proyecto de Hola. Este artículo muestra cómo toodeploy una aplicación web y la base de datos SQL tablas durante la implementación. Si va a implementar una máquina Virtual en lugar de una aplicación web, desea toorun parte del código en la máquina de hello como parte de la implementación. Hola el proceso de implementación de código para una aplicación web o para configurar una máquina Virtual es prácticamente igual Hola.

1. Agregar una solución de Visual Studio tooyour de proyecto. Haga clic en soluciones de Hola y seleccione **agregar** > **nuevo proyecto**.
   
    ![agregar proyecto](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Agregue una **aplicación web ASP.NET**. 
   
    ![agregar aplicación web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. Seleccione **MVC**.
   
    ![seleccionar MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Después de que Visual Studio crea la aplicación web, verá dos proyectos en soluciones de Hola.
   
    ![mostrar proyectos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Ahora, debe toomake seguro que es consciente del nuevo proyecto de hello el proyecto del grupo de recursos. Volver atrás tooyour proyecto del grupo de recursos (AzureResourceGroup1). Haga clic con el botón derecho en **Referencias** y seleccione **Agregar referencia**.
   
    ![Agregar referencia](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Seleccione el proyecto de aplicación web de Hola que ha creado.
   
    ![Agregar referencia](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Al agregar una referencia, vincular el proyecto de grupo recursos de toohello proyecto de aplicación web de Hola y establece automáticamente las tres propiedades de clave. Vea estas propiedades en hello **propiedades** ventana de referencia de Hola.
   
      ![ver referencia](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    Hola propiedades son:
   
   * Hola **propiedades adicionales** contiene el paquete de implementación web Hola ensayo ubicación a la que se inserta toohello almacenamiento de Azure. Tenga en cuenta Hola carpeta (ExampleApp) y el archivo (package.zip). Necesita tooknow estos valores porque se proporcionan como parámetros al implementar Hola aplicación. 
   * Hola **incluir ruta de acceso del archivo** contiene la ruta de acceso de Hola donde se crea el paquete de Hola. Hola **incluyen destinos** contiene comandos de Hola que se ejecuta la implementación. 
   * Hola valor predeterminado de **de compilación; Paquete** habilita Hola toobuild de implementación y crear un paquete de implementación web (package.zip).  
     
     No es necesario un perfil de publicación como implementación Hola obtiene información necesaria de Hola de paquete de hello propiedades toocreate Hola.
7. Retroceda tooWebSiteSQLDatabase.json y agregar una plantilla de toohello de recursos.
   
    ![agregar recurso](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. En esta ocasión, seleccione **Web Deploy para aplicaciones web**. 
   
    ![agregar implementación web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Volver a implementar el grupo de recursos recurso toohello de proyecto de grupo. Esta vez, hay algunos parámetros nuevos. No es necesario para los valores de tooprovide **_artifactsLocation** o **_artifactsLocationSasToken** porque Visual Studio genera automáticamente esos valores. Sin embargo, deberás tooset carpeta de Hola y ruta de acceso de la toohello de nombre de archivo que contiene el paquete de implementación de hello (se muestra como **ExampleAppPackageFolder** y **ExampleAppPackageFileName** Hola después de imagen ). Proporcionar valores de hello que vio anteriormente en Hola propiedades de referencia (**ExampleApp** y **package.zip**).
   
    ![agregar implementación web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Para hello **cuenta de almacenamiento de artefacto**, seleccione Hola uno implementado con este grupo de recursos.
10. Cuando haya finalizado la implementación de hello, seleccione la aplicación web en el portal de Hola. Seleccione Hola URL toobrowse toohello sitio.
    
     ![examinar sitio](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Tenga en cuenta que ha implementado correctamente la aplicación ASP.NET predeterminada hello.
    
     ![mostrar la aplicación implementada](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo administrar los recursos a través del portal de hello, consulte [Using Hola toomanage portal Azure de los recursos de Azure](resource-group-portal.md).
* toolearn más información sobre plantillas, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).

