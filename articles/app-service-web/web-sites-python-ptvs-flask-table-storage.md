---
title: aaaFlask y almacenamiento de tablas de Azure en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo toouse Hola Python Tools para Visual Studio toocreate una aplicación web matraz que almacena los datos en el almacenamiento de tabla de Azure e implementarlo tooAzure aplicación del servicio Web de aplicaciones."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Flask y Almacenamiento de tablas de Azure en Azure con Python Tools 2.2 para Visual Studio
En este tutorial, usaremos [Python Tools para Visual Studio] sondea de toocreate una sencilla aplicación web con una de las plantillas de ejemplo de Hola PTVS. Este tutorial también se encuentra disponible como [vídeo](https://www.youtube.com/watch?v=qUtZWtPwbTk).

aplicación web de Hello sondeos define una abstracción para el repositorio, por lo que puede cambiar fácilmente entre los distintos tipos de repositorios (en memoria, almacenamiento de tablas de Azure, MongoDB).

Obtendrá información sobre cómo cuenta toocreate un almacenamiento de Azure, cómo tooconfigure Hola toouse de aplicación web el almacenamiento de tabla de Azure y cómo toopublish Hola aplicación web demasiado[aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Vea hello [Centro para desarrolladores de Python] para ver más artículos que cubren el desarrollo de aplicaciones de Web del servicio de aplicación de Azure con PTVS mediante Bottle por sí solo, matraz y Django web marcos de trabajo, con los servicios de MongoDB, almacenamiento de tabla de Azure, MySQL y base de datos SQL. Aunque en este artículo se centra en el servicio de aplicaciones, los pasos de hello son similares al desarrollar [servicios en la nube].

## <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2015
* [Python Tools 2.2 para Visual Studio]
* [Python Tools 2.2 para Visual Studio ejemplos VSIX]
* [Herramientas de Azure SDK para VS 2015]
* [Python 2.7 de 32 bits] o [Python 3.4 de 32 bits]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="create-hello-project"></a>Crear proyecto de hello
En esta sección, vamos a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo. Vamos a crear un entorno virtual e instalar los paquetes necesarios. A continuación, ejecutaremos la aplicación hello localmente mediante el repositorio de hello predeterminado en memoria.

1. En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.
2. Hola plantillas de proyecto de hello [Python Tools 2.2 para Visual Studio ejemplos VSIX] están disponibles en **Python**, **ejemplos**. Seleccione **sondeos matraz Web Project** y haga clic en Aceptar toocreate Hola proyecto.
   
     ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. Es posible que los paquetes externos tooinstall solicitadas. Seleccione **Instalar en un entorno virtual**.
   
     ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. Seleccione **Python 2.7** o **3.4 de Python** como intérprete base Hola.
   
     ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. Confirme que la aplicación hello funciona presionando `F5`. De forma predeterminada, la aplicación hello usa un repositorio en memoria que no requiere ninguna configuración. Todos los datos se pierde cuando hello web server está detenido.
6. Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo) y, a continuación, haga clic en un sondeo y vote.
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de almacenamiento de Azure
operaciones de almacenamiento de toouse, necesita una cuenta de almacenamiento de Azure. Siga estos pasos para crear una cuenta de almacenamiento.

1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com/).
2. Haga clic en hello **New** icono en la parte superior de hello deja de hello Portal, a continuación, haga clic en **datos + almacenamiento** > **cuenta de almacenamiento**. Haga clic en **crear**, a continuación, asigne un nombre único de cuenta de almacenamiento de Hola y crear un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para él.
   
      ![Creación rápida](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    Cuando se ha creado la cuenta de almacenamiento de hello, Hola **notificaciones** botón parpadeará en un color verde **correcto** y está abierta la hoja de la cuenta de almacenamiento de hello tooshow que pertenece toohello nuevo recurso de grupo, creado.
3. Haga clic en hello **teclas de acceso** parte de la hoja de la cuenta de almacenamiento de Hola. Tome nota del nombre de la cuenta de Hola y Hola key1.
   
      ![simétricas](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    Necesitamos esta información tooconfigure el proyecto en la sección siguiente de Hola.

## <a name="configure-hello-project"></a>Configurar proyecto Hola
En esta sección, vamos a configurar la cuenta de almacenamiento de aplicación toouse Hola que acabamos de crear. Veremos cómo tooobtain configuración de conexión de Hola Portal de Azure. A continuación, ejecutaremos aplicación hello localmente.

1. En Visual Studio, haga clic con el botón derecho en el Explorador de soluciones y seleccione **Propiedades**. Haga clic en hello **depurar** ficha.
   
     ![Configuración de depuración del proyecto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. Establecer valores de hello de variables de entorno requeridos por la aplicación hello en **Depurar comandos de servidor**, **entorno**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Este modo, establecerá las variables de entorno de hello cuando se **Iniciar depuración**. Si desea que Hola variables toobe establece cuando se **iniciar sin depurar**, Hola conjunto mismos valores en **ejecutar comando de servidor** también.
   
   Como alternativa, puede definir variables de entorno mediante el Panel de Control de Windows hello. Se trata de una mejor opción si desea tooavoid almacenar credenciales en el código fuente o archivo de proyecto. Tenga en cuenta que necesitará toorestart Visual Studio para la aplicación de hello nuevo entorno valores toobe toohello disponibles.
3. código de Hello que implementa el repositorio de almacenamiento de tablas Azure Hola se encuentra en **models/azuretablestorage.py**. Vea hello [documentación] para obtener más información acerca de cómo toouse servicio de tablas de Python.
4. Ejecutar la aplicación hello con `F5`. Sondeos que se crean con **crear sondeos de ejemplo** y datos de hello enviados votando se van a serializar en el almacenamiento de tabla de Azure.
   
   > [!NOTE]
   > Hola entorno Virtual de Python 2.7 puede producir una interrupción de excepción en Visual Studio.  Presione `F5` toocontinue cargar el proyecto web de Hola.
   > 
   > 
5. Examinar toohello **sobre** tooverify de página que Hola aplicación está usando hello **almacenamiento de tablas Azure** repositorio.
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Explorar Hola almacenamiento de tabla de Azure
Es fácil tooview y editar tablas de almacenamiento mediante el Explorador de nube en Visual Studio. En esta sección, vamos a usar contenido de hello tooview de explorador de servidores de las tablas de aplicación de sondeos de Hola.

> [!NOTE]
> Para ello, toobe de Microsoft Azure Tools instalado, que están disponibles como parte del programa Hola a [Azure SDK para .NET].
> 
> 

1. Abra **Cloud Explorer**. Expanda **Cuentas de almacenamiento**, su cuenta de almacenamiento y, después, **Tablas**.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Haga doble clic en hello **sondeos** o **opciones** tabla tooview Hola contenido de tabla de hello en una ventana de documento, así como agregar/quitar/editar entidades.
   
     ![Resultados de la consulta de tabla](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar hello web app tooAzure servicio de aplicaciones
Hello Azure SDK para .NET proporciona una manera sencilla de toodeploy su tooAzure de aplicación web servicio de aplicaciones.

1. En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **publicar**.
   
     ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Haga clic en **Aplicaciones web de Microsoft Azure**.
3. Haga clic en **New** toocreate una nueva aplicación web.
4. Rellene Hola después de campos y haga clic en **crear**.
   
   * **Nombre de aplicación web**
   * **Plan del Servicio de aplicaciones**
   * **Grupos de recursos**
   * **Región**
   * Deje **servidor de base de datos** establecido demasiado**ninguna base de datos**
5. Acepte todos los valores predeterminados y haga clic en **Publicar**.
6. El explorador web abrirá automáticamente aplicaciones web publicadas de toohello. Si examina toohello acerca de la página, verá que usa hello **en memoria** repositorio, no hello **almacenamiento de tablas Azure** repositorio.
   
   Eso es porque no se establecen variables de entorno de hello en la instancia de aplicaciones Web de hello en el servicio de aplicación de Azure, por lo que utiliza valores predeterminados de hello especificados en **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Configurar la instancia de aplicaciones Web de Hola
En esta sección, vamos a configurar las variables de entorno para la instancia de aplicaciones Web de Hola.

1. En [Portal de Azure](https://portal.azure.com), abra la hoja de la aplicación hello web haciendo clic en **examinar** > **servicios de aplicaciones** > el nombre de la aplicación web.
2. En la hoja de la aplicación web, haga clic en **Toda la configuración** y en **Configuración de la aplicación**.
3. Desplácese hacia abajo toohello **configuración de la aplicación** sección y establecer valores de hello para **repositorio\_nombre**, **almacenamiento\_nombre** y  **ALMACENAMIENTO\_clave** tal y como se describe en hello **configurar proyectos de hello** sección anterior.
   
     ![Configuración de la aplicación](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Haga clic en **Save**(Guardar). Después de que ha recibido notificaciones de Hola que se aplicaran los cambios de hello, haga clic en **examinar** desde la hoja principal de hello Web app.
5. Debería ver el trabajo de aplicación web de hello según lo esperado, con hello **almacenamiento de tablas Azure** repositorio.
   
   ¡Enhorabuena!
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a>Pasos siguientes
Siga estos toolearn de vínculos más información acerca de Python Tools para Visual Studio, matraz y el almacenamiento de tabla de Azure.

* [Documentación sobre Python Tools para Visual Studio]
  * [Proyectos web]
  * [Proyectos de servicio en la nube]
  * [Depuración remota en Microsoft Azure]
* [Documentación de Flask]
* [Almacenamiento de Azure]
* [SDK de Azure para Python]
* [¿Cómo tooUse Hola servicio de almacenamiento de tabla de Python]

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centro para desarrolladores de Python]: /develop/python/
[servicios en la nube]: ../cloud-services/cloud-services-python-ptvs.md
[documentación]:../cosmos-db/table-storage-how-to-use-python.md
[¿Cómo tooUse Hola servicio de almacenamiento de tabla de Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK para .NET]: http://azure.microsoft.com/downloads/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 para Visual Studio ejemplos VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Herramientas de Azure SDK para VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs
[Documentación de Flask]: http://flask.pocoo.org/
[Depuración remota en Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Proyectos web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Proyectos de servicio en la nube]: http://go.microsoft.com/fwlink/?LinkId=624028
[Almacenamiento de Azure]: http://azure.microsoft.com/documentation/services/storage/
[SDK de Azure para Python]: https://github.com/Azure/azure-sdk-for-python
