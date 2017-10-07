---
title: Servicios de entrega de aaaContinuous para la nube con Visual Studio Online | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset la entrega continua de Azure en la nube aplicaciones sin guardar archivos de configuración de servicio de almacenamiento toohello clave de diagnóstico"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely guardar en la nube servicios de almacenamiento de información clave de diagnóstico y tooAzure de integración continua el programa de instalación e implementación mediante Visual Studio Online
 Hoy en día es un proyectos de código fuente de tooopen práctica común. Guardar los secretos de aplicación en archivos de configuración ya no es una práctica segura, ya que se producen vulnerabilidades de seguridad procedentes de los secretos que se filtran desde los controles de código fuente públicos. Almacenamiento secreto como texto no cifrado en un archivo en una canalización de integración continua no es segura ya sea porque pudieron ser servidores de compilación los recursos compartidos en el entorno de nube de Hola. Este artículo explica cómo Visual Studio y Visual Studio Online mitiga los riesgos de seguridad de Hola durante el desarrollo y el proceso de integración continua.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Eliminación del secreto de la clave de almacenamiento de la información de diagnóstico del archivo de configuración de proyecto
La extensión de diagnósticos de Cloud Services requiere Azure Storage para guardar los resultados de diagnóstico. Anteriormente la cadena de conexión de almacenamiento de Hola se especifica en archivos de configuración (.cscfg) de servicios en la nube de Hola y podría activarse en el control de toosource. En la versión más reciente de Azure SDK de hello hemos cambiado almacén tooonly Hola comportamiento que una parcial cadena de conexión con la clave de hello reemplazado por un símbolo (token). Hola pasos describe el funcionamiento de nuevas herramientas de servicios en la nube hello:

### <a name="1-open-hello-role-designer"></a>1. Abra el Diseñador de roles de Hola
* Haga doble clic o haga clic con el botón secundario en un diseñador de roles de tooopen de rol de servicios en la nube

![Abra el diseñador de roles][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. En la sección de diagnósticos, se ha agregado una nueva casilla de verificación "Don’t remove storage key secret from project" (No quitar secreto de la clave de almacenamiento del proyecto)
* Si usas el emulador de almacenamiento local de hello, esta casilla está deshabilitada porque no hay ningún secreto toomanage de cadena de conexión local de hello, que es UseDevelopmentStorage = true.

![La cadena de conexión del emulador de almacenamiento local no es un secreto][1]

* Si va a crear un nuevo proyecto, esta casilla de verificación estará desactivada de forma predeterminada. Esto da como resultado de sección de clave de almacenamiento de Hola de cadena de conexión de almacenamiento de hello seleccionado se reemplazan con un token. Hello valor del token de Hola se encontrará en la carpeta AppData móviles del usuario actual de hello, por ejemplo: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Tenga en cuenta esa carpeta user\AppData de hello es cuyo acceso esté controlado por inicio de sesión de usuario y se considera un lugar seguro toostore los secretos de desarrollo.
> 
> 

![La clave de almacenamiento se guarda en la carpeta del perfil de usuario][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Selección de la cuenta de almacenamiento de información de diagnóstico
* Seleccione una cuenta de almacenamiento del cuadro de diálogo de hello iniciada haciendo clic en "..." hello . Tenga en cuenta cómo cadena de conexión de almacenamiento de hello generado no tendrá clave de cuenta de almacenamiento de Hola.
* Por ejemplo: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Depurar el proyecto de Hola
* F5 toostart de depuración en Visual Studio. Todo lo que debería funcionar en hello igual manera que antes.
  ![Inicie la depuración localmente][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Publicación del proyecto desde Visual Studio
* Hola iniciar cuadro de diálogo Publicar y continúe con las instrucciones de inicio de sesión toopublish hello applicaion tooAzure.

### <a name="6-additional-information"></a>6. Información adicional
> Nota: el panel de configuración de hello en el Diseñador de roles de hello permanecerá tal cual por ahora. Si desea características de administración de secretos de toouse hello para el diagnóstico, vaya toohello configuraciones (pestaña).
> 
> 

![Incorporación de la configuración][4]

> Nota: Si está habilitada, se almacenará Hola Application Insights clave como texto sin formato. clave de Hola sólo se utiliza para el contenido de la carga de modo que ningún dato confidencial estarán en riesgo de comprometer.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Compilación y publicación de un proyecto de Cloud Services mediante plantillas de tareas en Visual Studio Online
* Hola pasos se muestra cómo usar tareas en línea de Visual Studio de proyectos de toosetup integración continua para servicios en la nube:
  ### <a name="1----obtain-a-vso-account"></a>1.    Obtenga una cuenta de VSO
* [Crear cuenta de Visual Studio Online] [ Create Visual Studio Online account] si aún no tiene uno
* [Crear proyecto de equipo] [ Create team project] en su cuenta en línea de Visual Studio

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Configuración del control de código fuente en Visual Studio
* Conectar el proyecto de equipo de tooa

![Conectar tooteam proyecto][5]

![Seleccione tooconnect de proyecto de equipo a][6]

* Agregar el control de toosource de proyecto

![Agregar proyecto toosource control][7]

![Carpeta de control de código fuente de mapa proyecto tooa][8]

* Compruebe el proyecto desde Team Explorer

![Compruebe en el control de toosource de proyectos][9]

### <a name="3----configure-build-process"></a>3.    Configuración del proceso de compilación
* Examinar el proyecto de equipo de tooyour y agregue un nuevo proceso de compilación, plantillas

![Agregue una nueva compilación][10]

* Seleccione una tarea de compilación

![Agregue una tarea de compilación][11]

![Seleccione la plantilla de tarea de compilación de Visual Studio][12]

* Edite la entrada de la tarea de compilación. Por favor, personalizar la generación de Hola que tenga parámetros según tooyour

![Configure la tarea de compilación][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Configure las variables de compilación

![Configure las variables de compilación][14]

* Agregar una caída de compilación de tooupload de tarea

![Elija publicar tarea de destino de compilación][15]

![Configure la tarea de publicación de destino de compilación][16]

* Ejecute hello compilación

![Ponga en cola la nueva compilación][17]

![Vea el resumen de compilación][18]

* Si se realiza correctamente la compilación de hello verá un toobelow similar de resultado

![Resultado de la compilación][19]

### <a name="4----configure-release-process"></a>4.    Configuración del proceso de lanzamiento
* Cree una nueva versión

![Cree una nueva versión][20]

* Seleccione la tarea de implementación de servicios de nube de Azure de hello

![Seleccione la tarea de implementación de Azure Cloud Services][21]

* Como no está activada la clave de cuenta de almacenamiento de hello en control toosource, necesitamos clave secreta de hello toospecify para configurar extensiones de diagnóstico. Expanda hello **opciones avanzadas para crear un nuevo servicio** sección y editar hello **claves de cuenta de almacenamiento de diagnósticos** proporcionados por el parámetro. Esta entrada se toma en varias líneas de par clave-valor en formato de Hola de **[RoleName]:$(StorageAccountKey)**

> Nota: si su cuenta de almacenamiento está por debajo de diagnóstico hello misma suscripción donde publicará la aplicación de servicios en la nube de hello, no tiene clave de hello tooenter de entrada de tarea de implementación de hello; implementación de Hola obtendrá mediante programación la información de almacenamiento Hola desde su suscripción
> 
> 

![Configuración de la tarea de implementación de Azure Cloud Services][22]

* Secreto de uso de compilación variables toosave claves de almacenamiento. toomask haga clic en una variable como secreto en el icono de candado de hello en hello derecha de hello las Variables de entrada

![Guardar las claves de almacenamiento en variables de compilación de secreto][23]

* Crear una versión e implementar su proyecto tooAzure

![Cree una nueva versión][24]

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la configuración de extensiones de diagnóstico para los servicios de nube de Azure, visite [habilitar diagnósticos en los servicios de nube de Azure con PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
