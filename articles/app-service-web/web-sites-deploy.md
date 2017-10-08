---
title: "aaaDeploy su aplicación de servicio de aplicación tooAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy su tooAzure aplicación servicio de aplicaciones."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>Implementar el servicio de aplicaciones de tooAzure de aplicación
En este artículo le ayudará a determinar Hola mejor opción toodeploy Hola archivos para su aplicación web, una aplicación móvil back-end o una aplicación de API demasiado[servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714)y, a continuación, le guía tooappropriate recursos con instrucciones específicas tooyour opción preferida.

## <a name="overview"></a>Descripción general de la implementación de Servicio de aplicaciones de Azure
Servicio de aplicaciones de Azure mantiene el marco de aplicación Hola automáticamente (ASP.NET, PHP, Node.js, etcetera). Algunos marcos de trabajo están habilitados de forma predeterminada, mientras que otros, como Java y Python, que tenga un tooenable de configuración de marca de verificación simple. Además, puede personalizar el marco de aplicación, como la versión PHP de Hola o bits de Hola de su tiempo de ejecución. Para obtener más información, consulte [Configuración de aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-configure.md).

Dado que no posee tooworry sobre el marco de aplicación de servidor o de hello web, implementar el servicio de aplicación tooApp consiste en implementar el código, los archivos binarios, archivos de contenido y su estructura de directorios respectivos, toohello [   **/site /wwwroot** directorio](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) en Azure (o hello **/sitio/wwwroot/App_Data/trabajos/** directorio de trabajos Web). App Service admite tres procesos de implementación diferentes. Todos los métodos de implementación de hello en este artículo usan uno de hello siguientes procesos: 

* [FTP o FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): Use los favoritos FTP o FTPS habilitada herramienta toomove su tooAzure archivos, desde [FileZilla](https://filezilla-project.org) tasky toofull IDE como [NetBeans](https://netbeans.org). Se trata estrictamente de un proceso de carga de archivos. El Servicio de aplicaciones no proporciona servicios adicionales, como control de versiones, administración de estructura de archivos, etc. 
* [Kudu (Git o Mercurial o OneDrive o Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu es hello [motor de implementación](https://github.com/projectkudu/kudu/wiki) de servicio de aplicaciones. Insertar el código tooKudu directamente desde cualquier repositorio. Kudu también proporciona servicios agregados cada vez que el código se inserta tooit, incluido el control de versiones, la restauración del paquete, MSBuild, y [web enlaces](https://github.com/projectkudu/kudu/wiki/Web-hooks) para la implementación continua y otras tareas de automatización. motor de implementación de Hello Kudu admite 3 diferentes tipos de orígenes de implementación:   
  
  * Sincronización de contenido de OneDrive y Dropbox.   
  * Implementación continua basada en repositorio con sincronización automática desde GitHub, Bitbucket y Visual Studio Team Services.  
  * Implementación basada en repositorio con sincronización manual desde Git local.  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): implementar código tooApp servicio directamente desde el Microsoft favoritos de las herramientas como Visual Studio mediante Hola mismo herramientas que automatiza servidores tooIIS de implementación. Esta herramienta es compatible con la implementación de solo diferencias, la creación de bases de datos, las transformaciones de cadenas de conexión, etc. Web Deploy difiere de Kudu en que la aplicación se compilan los archivos binarios antes de que implementa tooAzure. TooFTP similar, no hay servicios adicionales proceden de servicio de aplicaciones.

Las herramientas de desarrollo web más populares admiten uno o varios de estos procesos de implementación. Mientras que la elección de la herramienta hello determina los procesos de implementación de hello pueden aprovechar, hello funcionalidad de DevOps real a su disposición depende combinación Hola Hola del proceso de implementación y hello herramientas específicas elija. Por ejemplo, si ejecuta Web Deploy desde [Visual Studio con Azure SDK](#vspros), aunque no obtenga la automatización de Kudu, tendrá la restauración de paquetes y la automatización de MSBuild en Visual Studio. 

> [!NOTE]
> Estos procesos de implementación no realmente [aprovisionar recursos de Azure de Hola](../azure-resource-manager/resource-group-template-deploy-portal.md) que necesite la aplicación. Sin embargo, la mayoría de hello vinculado cómo-tooarticles muestra cómo tooprovision Hola aplicación e implementar su código tooit-to-end. También puede encontrar opciones adicionales para el aprovisionamiento de recursos de Azure en hello [automatizar la implementación mediante las herramientas de línea de comandos](#automate) sección.
> 
> 

## <a name="ftp"></a>Implementación manual mediante la carga de archivos con FTP
Si estás usado toomanually copiar el servidor de web tooa contenido web, puede usar un [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) archivos de toocopy de utilidad, como el Explorador de Windows o [FileZilla](https://filezilla-project.org/).

los profesionales de TI de Hola de copiar manualmente los archivos son:

* La familiaridad y la complejidad mínima de las herramientas de FTP. 
* Se sabe exactamente dónde van los archivos.
* Mayor seguridad con FTPS.

inconvenientes de Hola de copiar manualmente los archivos son:

* Tener tooknow cómo toodeploy directorios de los archivos toohello correcto en el servicio de aplicaciones. 
* No hay control de versiones para la reversión cuando se producen errores.
* No existe un historial integrado de las implementaciones para solucionar problemas con la implementación.
* Posible implementación mucho tiempo de espera porque muchas herramientas FTP no proporcionan la copia solo diferencias y solo tiene que copiar todos los archivos de saludo.  

### <a name="howtoftp"></a>¿Cómo tooupload archivos con FTP
Hola [Portal de Azure](https://portal.azure.com) proporciona toda la información de hello necesita directorios de la aplicación de tooconnect tooyour mediante FTP o FTPS.

* [Implementar el servicio de aplicaciones de app tooAzure mediante FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Implementación mediante sincronización con una carpeta en la nube
Una buena alternativa demasiado[copiar los archivos manualmente](#ftp) está sincronizando archivos y carpetas tooApp servicio desde un servicio de almacenamiento en la nube como OneDrive y Dropbox. Sincronizando con una carpeta en la nube utiliza el proceso de Kudu de hello para la implementación (vea [visión general de los procesos de implementación](#overview)).

los profesionales de TI de Hola de sincronización con una carpeta en la nube son:

* Sencillez de la implementación Servicios como OneDrive y Dropbox proporcionan clientes de sincronización de escritorio, por lo que el directorio de trabajo local también es el directorio de implementación.
* Implementación con un solo clic.
* Toda la funcionalidad de motor de implementación de hello Kudu está disponible (por ejemplo, la restauración del paquete, automatización).

inconvenientes de Hola de sincronización con una carpeta en la nube son:

* No hay control de versiones para la reversión cuando se producen errores.
* No hay implementación automatizada, se requiere la sincronización manual.

### <a name="howtodropbox"></a>¿Cómo toodeploy por la sincronización con una carpeta en la nube
Hola [Portal de Azure](https://portal.azure.com), puede designar una carpeta para la sincronización de contenido en el almacenamiento en nube OneDrive o Dropbox, trabajar con el código de la aplicación y el contenido de esa carpeta y haga clic en sincronizar tooApp servicio con hello de un botón.

* [Sincronizar el contenido de un tooAzure de carpeta servicio de aplicaciones de nube](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Implementación continua desde un servicio de control de código fuente basado en la nube
Si el equipo de desarrollo usa un servicio de administración (de servicios SCM) de código de origen en la nube como [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), o [BitBucket](https://bitbucket.org/), puede configurar la aplicación Toointegrate con su repositorio de servicio e implementar continuamente. 

los profesionales de TI de saludo de la implementación de un servicio de control de código fuente en la nube son:

* Reversión de tooenable de control de versión.
* La implementación continua de capacidad tooconfigure de Git (y Mercurial si procede) repositorios. 
* Implementación específica de la bifurcación, puede implementar diferentes bifurcaciones toodifferent [ranuras](web-sites-staged-publishing.md).
* Toda la funcionalidad de motor de implementación de hello Kudu está disponible (p. ej. el control de versiones de implementación, reversión, la restauración del paquete, automatización).

con Hello de la implementación de un servicio de control de código fuente en la nube es:

* Algunos conocimientos de servicio SCM correspondientes Hola necesario.

### <a name="vsts"></a>Cómo controlar el servicio toodeploy continuamente desde un origen en la nube
Hola [Portal de Azure](https://portal.azure.com), puede configurar una implementación continua desde GitHub y Bitbucket, Visual Studio Team Services.

* [Implementación continua tooAzure servicio de aplicaciones](app-service-continuous-deployment.md). 

toofind out cómo manualmente desde un repositorio de nube no aparece en una implementación continua tooconfigure Hola Portal de Azure (como [GitLab](https://gitlab.com/)), consulte [configurando la implementación continua mediante procesos manuales](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Implementación desde Git local
Si el equipo de desarrollo usa un servicio de administración (de servicios SCM) de código de origen local local basado en Git, puede configurar esto como un tooApp de origen de implementación servicio. 

Las ventajas de implementar desde un repositorio local Git son las siguientes:

* Reversión de tooenable de control de versión.
* Implementación específica de la bifurcación, puede implementar diferentes bifurcaciones toodifferent [ranuras](web-sites-staged-publishing.md).
* Toda la funcionalidad de motor de implementación de hello Kudu está disponible (p. ej. el control de versiones de implementación, reversión, la restauración del paquete, automatización).

La desventaja de implementar desde un repositorio local de Git es la siguiente:

* Algunos conocimientos de sistema de hello respectivo SCM que necesita.
* No hay ninguna solución llave en mano para la implementación continua. 

### <a name="vsts"></a>¿Cómo toodeploy de Git local
Hola [Portal de Azure](https://portal.azure.com), puede configurar la implementación de Git local.

* [TooAzure de implementación de Git local servicio de aplicaciones](app-service-deploy-local-git.md). 
* [Publicación de aplicaciones de tooWeb desde cualquier repositorio git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Implementación mediante un IDE
Si ya usas [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) con una [Azure SDK](https://azure.microsoft.com/downloads/), o como otros conjuntos de IDE [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), y [ IDEA IntelliJ](https://www.jetbrains.com/idea/), puede implementar tooAzure directamente desde el IDE. Esta opción es perfecta para un desarrollador individual.

Visual Studio es compatible con todos los procesos de implementación en tres (FTP, Git y Web Deploy), según sus preferencias, mientras que otros IDE puede implementar tooApp servicio si tienen integración FTP o Git (vea [visión general de los procesos de implementación](#overview)).

los profesionales de TI de saludo de la implementación con el IDE son:

* Minimizar potencialmente Hola conjunto de herramientas para el ciclo de vida de aplicación de extremo a extremo. Desarrollar, depurar, realizar un seguimiento e implementar su aplicación tooAzure sin necesidad de mover fuera el IDE. 

inconvenientes de saludo de la implementación con el IDE son:

* Mayor complejidad de las herramientas.
* Aún requiere un sistema de control de código fuente para un proyecto de equipo.

<a name="vspros"></a> Las ventajas adicionales de la implementación mediante Visual Studio con Azure SDK son las siguientes:

* Azure SDK hace de los recursos de Azure ciudadanos de primera clase en Visual Studio. Crear, eliminar, editar, iniciar y detener aplicaciones, base de datos SQL back-end de Hola de consulta, live-debug Hola aplicación de Azure y mucho más. 
* Edición en directo de archivos de código en Azure.
* Depuración en directo de aplicaciones en Azure.
* Explorador integrado de Azure.
* Implementación de solo diferencias. 

### <a name="vs"></a>¿Cómo toodeploy directamente desde Visual Studio
* [Introducción a Azure y ASP.NET](app-service-web-get-started-dotnet.md). ¿Cómo toocreate e implementar un proyecto web de ASP.NET MVC sencillo mediante Visual Studio y Web Deploy.
* [Cómo tooDeploy WebJobs de Azure con Visual Studio](websites-dotnet-deploy-webjobs.md). ¿Cómo tooconfigure aplicación de consola proyectos para que implemente como trabajos Web.  
* [Implementación web de ASP.NET con Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Una serie de tutoriales de 12 parte que cubre una gama más completa de las tareas de implementación de Hola a otros usuarios en esta lista. Se agregaron algunas características de implementación de Azure ya que se escribió tutorial Hola, pero notas que se agregan posteriormente explican qué es que faltan.
* [Implementar un tooAzure de sitio Web ASP.NET en Visual Studio 2012 desde un repositorio de Git directamente](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Explica cómo toodeploy web ASP.NET del proyecto en Visual Studio, mediante Hola Git toocommit complemento Hola código tooGit y conectarse Azure toohello repositorio de Git. A partir de Visual Studio 2013, la compatibilidad con Git está integrada y no requiere la instalación de un complemento.

### <a name="aztk"></a>Cómo usar toodeploy Hola kits de herramientas de Azure para Eclipse y IntelliJ IDEA
Microsoft hace posible toodeploy tooAzure de aplicaciones Web directamente desde Eclipse y IntelliJ a través de hello [Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse.md) y [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md). Hello tutoriales siguientes ilustran los pasos de Hola que intervienen en la implementación simple un simple "Hola" world aplicación Web tooAzure mediante el IDE:

* [Creación de una aplicación web Hello World para Azure en Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Este tutorial muestra cómo toouse Hola Kit de herramientas de Azure para Eclipse toocreate e implementar una aplicación de Hello World Web de Azure.
* [Creación de una aplicación web Hello World para Azure en IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Este tutorial muestra cómo toouse hello Azure Toolkit para IntelliJ toocreate e implementar una aplicación de Hello World Web de Azure.

## <a name="automate"></a>Automatización de la implementación mediante herramientas de línea de comandos
Si lo prefiere terminal de línea de comandos de hello como entorno de desarrollo de Hola de elección, puede crear scripts de tareas de implementación para la aplicación de servicio de aplicaciones con herramientas de línea de comandos. 

Las ventajas de la implementación con las herramientas de la línea de comandos son las siguientes:

* Habilita escenarios de implementación con script.
* Integra el aprovisionamiento de recursos de Azure y la implementación de código.
* Integra la implementación de Azure en los scripts de integración continua existentes.

Los inconvenientes de la implementación con las herramientas de la línea de comandos son las siguientes:

* No está indicado para los desarrolladores que prefieren GUI.

### <a name="automatehow"></a>La implementación de tooautomate con las herramientas de línea de comandos

Vea [automatizar la implementación de la aplicación de Azure con las herramientas de línea de comandos](app-service-deploy-command-line.md) para obtener una lista de tootutorials vínculos y herramientas de línea de comandos. 

## <a name="nextsteps"></a>Pasos siguientes
En algunos escenarios puede toobe tooeasily puede cambiar y hacia atrás entre un ensayo y una versión de producción de la aplicación. Para obtener más información, consulte [Implementación de ensayo en Web Apps](web-sites-staged-publishing.md).

Tener un plan de copia de seguridad y restauración es un elemento importante de cualquier flujo de trabajo de implementación. Para obtener información acerca de la copia de seguridad de servicio de aplicaciones de Hola y de la característica de restauración, vea [copias de seguridad de aplicaciones Web](web-sites-backup.md).  

Para obtener información acerca de cómo toomanage de Control de acceso basado en roles de Azure toouse tener acceso a la implementación del servicio tooApp, consulte [RBAC y publicación de aplicación Web](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

