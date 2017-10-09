---
title: aaaProvision e implementar microservicios predecible en Azure
description: "Obtenga información acerca de cómo toodeploy una aplicación formada por microservicios en el servicio de aplicación de Azure como una sola unidad y de una manera predecible con plantillas de grupo de recursos JSON y secuencias de comandos de PowerShell."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Aprovisionamiento e implementación predecibles de microservicios en Azure
Este tutorial se muestra cómo tooprovision e implementar una aplicación formada por [microservicios](https://en.wikipedia.org/wiki/Microservices) en [servicio de aplicaciones de Azure](/services/app-service/) como una sola unidad y de una manera predecible con plantillas de grupo de recursos JSON y Secuencias de comandos de PowerShell. 

Al aprovisionar e implementar aplicaciones de gran escala que se componen de microservicios tan desacoplada, repetibilidad y la previsibilidad son toosuccess fundamental. [Servicio de aplicaciones de Azure](/services/app-service/) permite microservicios toocreate que incluyen las aplicaciones web, aplicaciones móviles, aplicaciones de API y las aplicaciones lógicas. [El Administrador de recursos Azure](../azure-resource-manager/resource-group-overview.md) permite toomanage todos los microservicios hello como una unidad, junto con las dependencias de recursos como la configuración de control de origen y la base de datos. Ahora, también puede implementar esta aplicación mediante plantillas JSON y scripting sencillo de PowerShell. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Lo que hará
En el tutorial de hello, implementará una aplicación que incluye:

* Dos aplicaciones web (es decir, dos microservicios)
* Un base de datos SQL backend
* Configuración de aplicaciones, cadenas de conexión y control de código fuente
* Información sobre aplicaciones, alertas y configuración de autoescala

## <a name="tools-you-will-use"></a>Herramientas que va a utilizar
En este tutorial, utilizará Hola después de herramientas. Puesto que no es una discusión completa sobre las herramientas, voy escenario de toostick toohello-to-end y póngale un tooeach breve introducción, y dónde puede encontrar más información sobre él. 

### <a name="azure-resource-manager-templates-json"></a>Plantillas del Administrador de recursos de Azure (JSON)
Cada vez que cree una aplicación web en el servicio de aplicación de Azure, por ejemplo, Azure Resource Manager usa un grupo de recursos completo de JSON plantilla toocreate Hola con recursos de componente de Hola. Una plantilla compleja de hello [Azure Marketplace](/marketplace) como hello [WordPress escalable](/marketplace/partners/wordpress/scalablewordpress/) aplicación puede incluir la base de datos de MySQL de hello, cuentas de almacenamiento, Hola plan de servicio de aplicaciones, aplicación web de hello propio, reglas de alerta, aplicación configuración, la configuración de escalado automático y la más y todas estas plantillas son tooyou disponible a través de PowerShell. Para obtener información sobre cómo toodownload y usar estas plantillas, consulte [con Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).

Para obtener más información sobre plantillas de Azure Resource Manager hello, consulte [creación de plantillas de administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>SDK de Azure 2.6 para Visual Studio
Hello SDK más reciente contiene mejoras toohello compatibilidad con plantillas de administrador de recursos en el editor de JSON de Hola. Puede usar este tooquickly crear una plantilla de grupo de recursos desde el principio o abrir una plantilla existente de JSON (por ejemplo, una plantilla de la Galería descargado) para su modificación, rellenar el archivo de parámetros de hello e incluso implementar grupo de recursos de hello directamente desde un Azure Solución de grupo de recursos.

Para obtener más información, consulte [SDK de Azure 2.6 para Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 o posterior
A partir de la versión 0.8.0, hello Azure PowerShell instalación incluye el módulo de Azure Resource Manager de hello en suma toohello módulo de Azure. Este nuevo módulo permite la implementación de hello tooscript de grupos de recursos.

Para obtener más información, consulte [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Explorador de recursos de Azure
Esto [herramienta de vista previa](https://resources.azure.com) permite las definiciones de tooexplore Hola JSON de todos los grupos de recursos de hello en los recursos individuales hello y suscripción. En la herramienta hello, puede editar las definiciones de JSON de Hola de un recurso, eliminar toda una jerarquía de recursos y crear nuevos recursos.  Hola información inmediatamente disponible en esta herramienta es muy útil para la creación de plantillas, porque muestra qué propiedades debe tooset para un determinado tipo de recurso, hello corregir valores, etcetera. Incluso puede crear el grupo de recursos en hello [Portal de Azure](https://portal.azure.com/), a continuación, inspeccione sus definiciones de JSON en hello explorador herramienta toohelp templatize grupo de recursos de Hola.

### <a name="deploy-tooazure-button"></a>Botón tooAzure implementar
Si utiliza GitHub para control de código fuente, puede colocar una [implementar tooAzure botón](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) en el archivo Léame. MD, lo que permite un tooAzure de interfaz de usuario de implementación preparada. Aunque también puede hacer esto para cualquier aplicación web simple, puede ampliar este tooenable implantación de un grupo de recursos completo colocando un archivo azuredeploy.json en el directorio raíz del repositorio Hola. Se usará este archivo JSON, que contiene la plantilla de grupo de recursos de hello, por grupo de recursos Hola de hello implementar tooAzure botón toocreate. Para obtener un ejemplo, vea hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) ejemplo, que se va a utilizar en este tutorial.

## <a name="get-hello-sample-resource-group-template"></a>Obtener la plantilla de grupo de recursos de ejemplo de Hola
Ahora vamos a tooit derecho.

1. Navegue toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) ejemplo de servicio de aplicaciones.
2. En readme.md, haga clic en **implementar tooAzure**.
3. Se irán toohello [implementar en azure](https://deploy.azure.com) sitio y los parámetros de implementación de tooinput frecuentes. Tenga en cuenta que la mayoría de los campos de Hola se rellena con el nombre del repositorio de Hola y algunas cadenas aleatorias para usted. Puede cambiar todos los campos de hello si lo desea, pero cosas solo hello tiene tooenter son inicio de sesión de administración de SQL Server hello y la contraseña de hello, a continuación, haga clic en **siguiente**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. A continuación, haga clic en **implementar** proceso de implementación de toostart Hola. Una vez que toocompletion ejecuta el proceso de hello, haga clic en hello http://todoapp*XXXX*. Hola de azurewebsites.net vínculo toobrowse implementado la aplicación. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Hola UI sería un poco lento cuando examine primero tooit porque Hola aplicaciones simplemente iniciando, pero usted mismo que decida que es una aplicación totalmente funcional.
5. En página de implementar hello, haga clic en hello **administrar** vincular toosee Hola nueva aplicación Hola Portal de Azure.
6. Hola **Essentials** de lista desplegable, haga clic en el vínculo de grupo de recursos de Hola. Tenga en cuenta también que hello de la aplicación web ya está conectado toohello repositorio de GitHub en **proyecto externo**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. En la hoja de grupo de recursos de hello, tenga en cuenta que ya hay dos aplicaciones web y una base de datos de SQL en el grupo de recursos de Hola.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Todo lo que ha visto en unos minutos cortos es una aplicación totalmente implementado dos-microservicio, con todos los componentes de hello, dependencias, configuración, base de datos y publicación continua, configurar una orquestación automatizadas en el Administrador de recursos de Azure. Todo esto se realiza mediante dos elementos:

* botón de Hello implementar tooAzure
* azuredeploy.JSON en la raíz del repositorio de Hola

Puede implementar esta aplicación mismo decenas, cientos o miles de veces y tener Hola misma configuración cada vez. capacidad de predicción de Hello hello y capacidad de repetición de este enfoque permite toodeploy aplicaciones de gran tamaño con facilidad y de confianza.

## <a name="examine-or-edit-azuredeployjson"></a>Examine (o edite) AZUREDEPLOY.JSON
Ahora Echemos un vistazo a cómo se ha configurado el repositorio de GitHub de Hola. Va a usar el editor de JSON de hello en hello Azure .NET SDK, por lo que si no ha instalado todavía [.NET de Azure SDK 2.6](/downloads/), hágalo ahora.

1. Hola clon [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repositorio mediante la herramienta git favoritos. En la captura de pantalla de Hola a continuación, llevar a cabo esto Hola Team Explorer en Visual Studio 2013.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. En la raíz del repositorio de hello, abra azuredeploy.json en Visual Studio. Si no ve el panel de esquema de JSON de hello, deberá tooinstall .NET SDK de Azure.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

Estoy no continuo toodescribe todos los detalles del formato JSON de hello, pero Hola [más recursos](#resources) sección hay vínculos para obtener información sobre el idioma de plantilla de grupo de recursos de Hola. En este caso, simplemente voy tooshow Hola interesantes características que pueden ayudarle a empezar a trabajar en la creación de su propia plantilla personalizada para la implementación de la aplicación.

### <a name="parameters"></a>parameters
Eche un vistazo a toosee de sección de parámetros de Hola que la mayoría de estos parámetros son qué hello **implementar tooAzure** botón le pide que tooinput. sitio de Hello detrás de hello **implementar tooAzure** botón rellena Hola entrada interfaz de usuario mediante parámetros de hello definidos en azuredeploy.json. Estos parámetros se usan en las definiciones de recursos de hello, como nombres de recursos, los valores de propiedad, etcetera.

### <a name="resources"></a>Recursos
En el nodo de recursos de hello, puede ver que se definen 4 recursos de nivel superior, incluidos los dos aplicaciones web, un plan de servicio de aplicaciones y una instancia de SQL Server. 

#### <a name="app-service-plan"></a>Plan de App Service
Comencemos con un recurso de nivel de raíz simple en hello JSON. Hola esquema JSON, haga clic en plan de servicio de aplicaciones de hello denominado **[hostingPlanName]** toohighlight Hola código JSON correspondiente. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Tenga en cuenta que hello `type` elemento especifica la cadena de Hola para un plan de servicio de aplicaciones (se llama a una granja de servidores hace un tiempo de long, long) y otros elementos y propiedades se rellenan con los parámetros de hello definidos en el archivo JSON de hello y no tiene este recurso todos los recursos anidados.

> [!NOTE]
> Tenga en cuenta también ese valor Hola de `apiVersion` indica qué versión de definición de recursos JSON hello toouse de API de REST Hola con y puede afectar a cómo se deben dar formato a los recursos de hello dentro de Hola de Azure `{}`. 
> 
> 

#### <a name="sql-server"></a>SQL Server
A continuación, haga clic en el recurso de SQL Server de hello denominado **SQLServer** Hola esquema JSON.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Hola nota siguiente sobre Hola resalta código JSON:

* uso de Hola de parámetros garantiza que recursos Hola creado se denominado y configurados de forma que hace que sean coherentes entre sí.
* Hola recursos de SQL Server tiene dos recursos anidados, cada uno tiene un valor diferente para `type`.
* Hola anidados recursos dentro de `“resources”: […]`, donde se definen la base de datos de Hola y reglas de firewall de hello, tener un `dependsOn` elemento que especifica el Id. de recurso de Hola de recurso de SQL Server de nivel de raíz de Hola. Esto indica a Azure Resource Manager, "antes de crear este recurso, que otro recurso debe existir; y si ese otro recurso está definido en la plantilla de hello, a continuación, cree que una primero".
  
  > [!NOTE]
  > Para obtener información detallada sobre cómo hello toouse `resourceId()` función, vea [funciones de plantilla de administrador de recursos de Azure](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* Hola efecto de hello `dependsOn` elemento es que el Administrador de recursos de Azure puede saber qué recursos se pueden crear en paralelo y qué recursos deben crearse de forma secuencial. 

#### <a name="web-app"></a>Aplicación web
Ahora, pasemos toohello real aplicaciones web, que son más complicadas. Haga clic en aplicación web de hello [variables('apiSiteName')] en hello esquema JSON toohighlight su código JSON. Observará que las cosas se están poniendo mucho más interesantes. Para este propósito, explicaré características Hola uno a uno:

##### <a name="root-resource"></a>Recurso raíz
aplicación web de Hello depende de dos recursos distintos. Esto significa que Azure Resource Manager creará la aplicación web de hello solo después de ambos Hola hello instancia de SQL Server y el plan de servicio de aplicaciones se crean.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>Configuración de la aplicación
configuración de la aplicación Hello también se define como un recurso anidado.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

Hola `properties` (elemento) para `config/appsettings`, tiene dos opciones de aplicación en formato de hello `“<name>” : “<value>”`.

* `PROJECT`es un [configuración KUDU](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) qué toouse del proyecto de implementación de Azure que indique en una solución de Visual Studio de varios proyecto. Se mostrará más adelante cómo se configura el control de código fuente, pero puesto que hello ToDoApp código en una solución de Visual Studio de varios proyecto, necesitamos esta configuración.
* `clientUrl`es simplemente una aplicación establecer ese código de la aplicación hello usa.

##### <a name="connection-strings"></a>Cadenas de conexión
las cadenas de conexión de Hello también se definen como un recurso anidado.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

Hola `properties` (elemento) para `config/connectionstrings`, cada cadena de conexión también se define como un par de nombre: valor con formato específico de Hola de `“<name>” : {“value”: “…”, “type”: “…”}`. Para hello `type` elemento, los valores posibles son `MySql`, `SQLServer`, `SQLAzure`, y `Custom`.

> [!TIP]
> Para obtener una lista de tipos de cadena de conexión de hello definitiva, ejecute hello siguiente comando de PowerShell de Azure: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Control de código fuente
configuración de control de código fuente de Hello también se define como un recurso anidado. Administrador de recursos de Azure usa esta publicación continua de tooconfigure de recursos (vea salvedad en `IsManualIntegration` más adelante) y también tookick desactivar implementación Hola del código de aplicación automáticamente durante el procesamiento de Hola de archivo JSON de hello.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`y `branch` deben ser muy intuitiva y debe apuntar toohello Git nombre hello y repositorio de hello bifurcación toopublish desde. De nuevo, se definen mediante parámetros de entrada. 

Tenga en cuenta en hello `dependsOn` elemento que, en suma toohello web recursos de aplicación, `sourcecontrols/web` depende también de `config/appsettings` y `config/connectionstrings`. Esto es porque una vez `sourcecontrols/web` está configurado, Hola proceso de implementación de Azure intentará automáticamente toodeploy, generar e iniciar el código de la aplicación hello. Por lo tanto, insertar esta Ayuda de dependencia Asegúrese de que esa aplicación hello tiene acceso toohello requiere configuración de la aplicación y las cadenas de conexión antes de ejecuta el código de la aplicación hello. 

> [!NOTE]
> Tenga en cuenta también que `IsManualIntegration` se establece demasiado`true`. Esta propiedad es necesaria en este tutorial, ya que no pertenezcan realmente repositorio de GitHub de hello y, por tanto, realmente no puede conceder permiso tooAzure tooconfigure continua la publicación de [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (es decir, inserción automática repositorio de actualizaciones tooAzure). Puede usar el valor predeterminado de hello `false` para el repositorio especificado de hello solo si ha configurado las credenciales de GitHub del propietario de Hola Hola [portal de Azure](https://portal.azure.com/) antes. En otras palabras, si ha configurado tooGitHub de control de código fuente o BitBucket para cualquier aplicación Hola [Portal de Azure](https://portal.azure.com/) anteriormente, con el usuario las credenciales, Azure se Recordar credenciales hello y utilizarlos para implementar cualquier aplicación del GitHub o BitBucket Hola futuras. Sin embargo, si aún no lo ha hecho esto todavía, se producirá un error en la implementación de plantilla JSON de hello cuando Azure Resource Manager trata la configuración de control de código fuente de la aplicación de tooconfigure hello web porque no se puede iniciar sesión en GitHub o BitBucket con credenciales del propietario del repositorio de Hola.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Comparar Hola JSON plantilla con el grupo de recursos implementados
En este caso, puede ir a través de módulos de la aplicación de todos los hello web Hola [Portal de Azure](https://portal.azure.com/), pero no hay otra herramienta que es igual que resulta muy útil, si no más. Vaya toohello [Explorador de recursos de Azure](https://resources.azure.com) herramienta de vista previa, que proporciona una representación JSON de todos los grupos de recursos de hello en sus suscripciones, ya que existen realmente en hello Azure back-end. También puede ver cómo JSON jerarquía del grupo de recursos de hello en Azure corresponde con jerarquía Hola del archivo de plantilla de Hola que ha usado toocreate lo.

Por ejemplo, al ir toohello [Explorador de recursos de Azure](https://resources.azure.com) herramienta y expanda los nodos de hello en el Explorador de hello, veo Hola grupo de recursos de nivel de raíz de Hola que se recopilan en sus tipos de recursos respectivas.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Si se profundiza tooa web app, debe ser capaz de toosee web app configuración detalles similares toohello siguiente captura de pantalla:

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

De nuevo, hello recursos anidados deben tener un toothose muy similar de jerarquía en el archivo de plantilla JSON y debería ver la configuración de la aplicación hello, las cadenas de conexión, etc., refleja correctamente en hello JSON. ausencia de Hola de estas opciones puede indicar un problema con el archivo JSON y puede ayudarle a solucionar el archivo de plantilla JSON.

## <a name="deploy-hello-resource-group-template-yourself"></a>Implementar la plantilla de grupo de recursos de hello usted mismo
Hola **implementar tooAzure** botón es grande, pero permite toodeploy plantilla de grupo de recursos de hello en azuredeploy.json sólo si ya ha insertado azuredeploy.json tooGitHub. Hello Azure SDK para .NET también proporciona herramientas de Hola para toodeploy cualquier archivo de plantilla JSON directamente desde el equipo local. toodo, a continuación siga los pasos hello:

1. En Visual Studio, haga clic en **Archivo** > **Nuevo** > **proyecto**.
2. Haga clic en **Visual C#** > **Nube** >  **&gt; Grupo de recursos de Azure** y, a continuación, haga clic en **Aceptar**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. En **Seleccionar plantilla de Azure**, seleccione **Plantilla en blanco** y haga clic en **Aceptar**.
4. Arrastre azuredeploy.json hello **plantilla** carpeta del nuevo proyecto.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. Desde el Explorador de soluciones, abra azuredeploy.json Hola copiado.
6. Solo para simplificar Hola demostración de hello, vamos a agregar algunos archivos JSON tooour recursos de Application Insight haciendo clic en **Agregar recurso**. Si le interesa acaba de implementar el archivo JSON de hello, omitir toohello implementar pasos.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Seleccione **Application Insights para Web Apps**; a continuación, asegúrese de que hay un plan de App Service y una aplicación web seleccionados y, a continuación, haga clic en **Agregar**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   Ahora deberá ser capaz de toosee varios recursos nuevos que, según los recursos de Hola y lo que hace, tienen dependencias en cualquier aplicación de servicio de aplicaciones plan o hello web Hola. Estos recursos no están habilitados por su definición existente y se vayan toochange que.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. Hola esquema JSON, haga clic en **appInsights escalado automático** toohighlight su código JSON. Se trata de hello configuración para el plan de servicio de aplicaciones de escala.
9. En Hola código resaltado de JSON, busque hello `location` y `enabled` propiedades y configúrelos como se muestra a continuación.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. Hola esquema JSON, haga clic en **CPUHigh appInsights** toohighlight su código JSON. Se trata de una alerta.
11. Busque hello `location` y `isEnabled` propiedades y configúrelos como se muestra a continuación. Hola igual para hello otras tres alertas (bombillas púrpuras).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. Ahora está listo toodeploy. Haga clic en proyecto de Hola y seleccione **implementar** > **nueva implementación**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Inicie sesión en su cuenta de Azure si aún no lo ha hecho.
14. Seleccione un grupo de recursos existente en su suscripción o cree uno nuevo y seleccione **azuredeploy.json**, y, a continuación, haga clic en **Editar parámetros**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    Ahora podrá tooedit capaz de todos los parámetros de hello definidos en el archivo de plantilla de hello en una tabla "nice". Los parámetros que definen los valores predeterminados ya tendrán sus valores predeterminados y los parámetros que definen una lista de valores permitidos se mostrarán como menús desplegables.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Rellene todos los parámetros vacía hello y usar hello [dirección de repositorio de GitHub para ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) en **dirección URL del repositorio**. A continuación, haga clic en **Guardar**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > El escalado automático es una característica que se ofrecen en **estándar** nivel o superior y el nivel de plan alertas son características proporcionadas en **básica** nivel o una versión posterior, deberá hello tooset **sku** parámetro demasiado**estándar** o **Premium** en orden toosee todos los nuevos detalles de aplicaciones recursos claro seguridad.
    > 
    > 
16. Haga clic en **Implementar**. Si seleccionó **guardar contraseñas**, Hola contraseña se guardará en el archivo de parámetros de hello **en texto sin formato**. En caso contrario, se le preguntará contraseña de base de datos de tooinput Hola durante el proceso de implementación de Hola.

¡Ya está! Ahora debe toogo toohello [Portal de Azure](https://portal.azure.com/) hello y [Explorador de recursos de Azure](https://resources.azure.com) herramienta toosee Hola nuevas alertas y configuración de escalado automático agrega tooyour JSON implementado la aplicación.

Los pasos de esta sección consigue principalmente siguiente hello:

1. Archivo de plantilla de hello preparada
2. Crea un toogo de archivo del parámetro con el archivo de plantilla de hello
3. Archivo de plantilla de hello implementado con el archivo de parámetros de Hola

último paso de Hello fácilmente se realiza mediante un cmdlet de PowerShell. toosee lo hizo Visual Studio cuando implementa la aplicación, abra Scripts\Deploy-AzureResourceGroup.ps1. Hay una gran cantidad de código, existen, pero simplemente voy a toohighlight todo código pertinente Hola necesitará toodeploy Hola plantilla archivo con el archivo de parámetros de Hola.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

Hola cmdlet última, `New-AzureResourceGroup`, es hello que realmente realiza la acción de Hola. Todo esto debería mostrar tooyou que, con la Ayuda de Hola de herramientas, es relativamente sencillo toodeploy su aplicación en la nube es predecible. Cada vez que se ejecuta el cmdlet de hello en hello Hola a misma plantilla con el mismo archivo de parámetros, se vayan tooget Hola el mismo resultado.

## <a name="summary"></a>Resumen
En DevOps, repetibilidad y la previsibilidad son claves tooany implementar correctamente una aplicación de gran escala formada por microservicios. En este tutorial, ha implementado un tooAzure de aplicación de dos microservicio como un único grupo de recursos mediante la plantilla de hello Azure Resource Manager. Con suerte, le ha concedido Hola conocimiento necesita en toostart orden convertir su aplicación en Azure en una plantilla y puede aprovisionar e implementar de forma predecible. 

## <a name="next-steps"></a>Pasos siguientes
Obtener información sobre cómo demasiado[aplicar las metodologías de agile y continuamente publicar la aplicación de microservicios con facilidad](app-service-agile-software-development.md) y técnicas de implementación como avanzadas [implementación programa Windows Insider](app-service-web-test-in-production-controlled-test-flight.md) fácilmente.

<a name="resources"></a>

## <a name="more-resources"></a>Más recursos
* [Idioma de la plantilla del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Funciones de la plantilla del Administrador de recursos de Azure](../azure-resource-manager/resource-group-template-functions.md)
* [Implementación de una aplicación con la plantilla del Administrador de recursos de Azure](../azure-resource-manager/resource-group-template-deploy.md)
* [Uso de Azure PowerShell con el Administrador de recursos de Azure](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Solución de problemas de implementaciones de grupo de recursos en Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md)

