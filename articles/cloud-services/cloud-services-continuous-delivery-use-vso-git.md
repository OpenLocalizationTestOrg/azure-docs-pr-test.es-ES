---
title: entrega aaaContinuous con Git y Visual Studio Team Services en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure su Visual Studio Team Services proyectos de equipo de toouse Git tooautomatically compilar e implementar la característica de la aplicación Web de toohello en los servicios en la nube o de servicio de aplicaciones de Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>TooAzure la entrega continua con Visual Studio Team Services y Git
Puede usar toohost de proyectos de equipo de Visual Studio Team Services un repositorio Git para el código fuente y automáticamente de compilación e implementar tooAzure las aplicaciones web o servicios en la nube siempre que realice una inserción un repositorio de toohello de confirmación.

Necesitará Visual Studio 2013 y hello Azure SDK instalado. Si ya no tiene Visual Studio 2013, descárguelo eligiendo hello **empiece de forma gratuita** vincular en [www.visualstudio.com](http://www.visualstudio.com). Instalación hello Azure SDK desde [aquí](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Necesita un toocomplete de cuenta de Visual Studio Team Services este tutorial: puede [abrir una cuenta de Visual Studio Team Services gratis](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset seguridad un tooautomatically de servicio de nube compilar e implementar tooAzure mediante el uso de Visual Studio Team Services, siga estos pasos.

## <a name="1-create-a-git-repository"></a>1: Creación de un repositorio Git
1. Si no tiene una cuenta de Visual Studio Team Services, puede obtenerla [aquí](http://go.microsoft.com/fwlink/?LinkId=397665). Cuando cree un proyecto de equipo, elija Git como el sistema de control de código fuente. Siga el proyecto de equipo de hello instrucciones tooconnect Visual Studio tooyour.
2. En **Team Explorer**, elija hello **clonar este repositorio** vínculo.
   
    ![][3]
3. Especificar ubicación de Hola de copia local de hello y, a continuación, elija hello **clon** botón.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: crear un proyecto y confirmar toohello repositorio
1. En **Team Explorer**, Hola **soluciones** sección, elija hello **New** vincular toocreate un proyecto nuevo en el repositorio local de Hola.
   
    ![][4]
2. Puede implementar una aplicación web o un servicio de nube (aplicación de Azure) por hello siguiente los pasos de este tutorial. Cree un proyecto nuevo de Servicio en la nube de Azure o un proyecto nuevo de MVC de ASP.NET. Asegúrese de que el destino del proyecto de Hola Hola .NET Framework 4 o posterior. Si va a crear un proyecto de servicio en la nube, agregue un rol web y un rol de trabajo de ASP.NET MVC.
   Si desea toocreate una aplicación web, elija hello **aplicación Web ASP.NET** plantilla de proyecto y, a continuación, elija **MVC**. Para obtener más información, consulte [Creación de una aplicación web ASP.NET en el Servicio de aplicaciones de Azure](../app-service-web/app-service-web-get-started-dotnet.md) .
3. Abra el acceso directo de hello para la solución de Hola y elija **confirmar**.
   
    ![][7]
4. Si se trata de hello primera vez que se ha usado Git en Visual Studio Team Services, necesitará tooprovide algunos tooidentify información por sí mismo en Git. Hola **cambios pendientes** área no cliente de **Team Explorer**, escriba el nombre de usuario y dirección de correo electrónico. Escriba un comentario para la confirmación de hello y, a continuación, elija hello **confirmación** botón.
   
    ![][8]
5. Tenga en cuenta tooinclude de opciones de Hola o excluir cambios específicos cuando protegen. Si cambia de Hola quiere que se excluyen, elija **incluyen todos los**.
6. Ha ahora Hola confirma los cambios en una copia local del repositorio de Hola. A continuación, sincroniza esos cambios con el servidor de hello eligiendo hello **sincronización** vínculo.

## <a name="3-connect-hello-project-tooazure"></a>3: conectar Hola proyecto tooAzure
1. Ahora que tiene un repositorio de Git en Visual Studio Team Services con algún código fuente en ella, está listo tooconnect su tooAzure de repositorio de git.  Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), seleccione la aplicación web o servicio de nube, o cree uno nuevo eligiendo Hola + situado en inferior izquierda de Hola y elegir **servicio de nube** o **Web App**y, a continuación, **creación rápida**.
   
    ![][9]
2. Servicios de nube, elija hello **configurar la publicación con Visual Studio Team Services** vínculo. Para las aplicaciones web, elija hello **configurar implementación desde control de código fuente** vínculo.
   
    ![][10]
3. En el Asistente de hello, escriba el nombre de hello de la cuenta de Visual Studio Team Services en el cuadro de texto de Hola y elija hello **autorizar ahora** vínculo. Toosign en que se le pida.
   
    ![][11]
4. Hola **solicitud de conexión** cuadro de diálogo emergente, elija **Accept** tooauthorize tooconfigure Azure su equipo de proyecto en Visual Studio Team Services.
   
    ![][12]
5. Si la autorización se realiza correctamente, verá una lista desplegable que contiene los proyectos del equipo de Visual Studio Team Services.  Seleccionar nombre de hello del proyecto de equipo que creó en los pasos anteriores de Hola y elija el botón de marca de verificación del Asistente de Hola.
   
    ![][13]
   
    Hola próxima vez que se insertará un repositorio de tooyour de confirmación, Visual Studio Team Services compilará e implementará el proyecto tooAzure.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: Desencadenamiento de una recompilación y nueva implementación del proyecto
1. En Visual Studio, abra un archivo y cámbielo. Por ejemplo, cambie el archivo hello `_Layout.cshtml` en vistas de hello\\carpeta compartida en un rol web MVC.
   
    ![][17]
2. Editar texto de pie de página de hello para el sitio de Hola y guarde el archivo hello.
   
    ![][18]
3. En **el Explorador de soluciones**, abra el menú contextual de Hola para hello nodo de la solución, el nodo del proyecto u Hola de archivos que se modificó y, a continuación, elija **confirmar**.
4. Escriba un comentario y elija **Confirmar**.
   
    ![][20]
5. Elija hello **sincronización** vínculo.
   
    ![][38]
6. Elija hello **Push** vincular toopush el repositorio de toohello de confirmación en Visual Studio Team Services. (También puede usar hello **sincronización** botón toocopy el repositorio de toohello confirmaciones. Hola diferencia es que **sincronización** también extrae Hola cambios más recientes desde el repositorio de Hola.)
   
    ![][39]
7. Elija hello **principal** botón tooreturn toohello **Team Explorer** página principal.
   
    ![][21]
8. Elija **compilaciones** tooview Hola se basa en curso.
   
    ![][22]
   
    **Team Explorer** indica que se ha desencadenado una compilación para su protección.
   
    ![][23]
9. tooview un registro detallado que Hola compilación progresa, haga doble clic en nombre de Hola de compilación de hello en curso.
10. Mientras compilación Hola está en curso, eche un vistazo en la definición de compilación de Hola que se creó cuando se usa Hola Asistente toolink tooAzure.  Abra el menú contextual de Hola de definición de compilación de Hola y elija **Editar definición de compilación**.
    
    ![][25]
11. Hola **desencadenador** pestaña, verá que definición de compilación de Hola se establece toobuild en cada en el repositorio, de forma predeterminada. (Para un servicio de nube, Visual Studio Team Services genera e implementa Hola bifurcación principal toohello automáticamente, el entorno de ensayo. Todavía tiene toodo un sitio de paso manual toodeploy toohello en vivo. Para una aplicación web que no tiene el entorno de ensayo, se implementa la bifurcación principal de hello directamente toohello live sitio.
    
    ![][26]
12. Hola **proceso** ficha, puede ver el entorno de implementación de Hola se establece toohello nombre de la aplicación web o servicio de nube.
    
     ![][27]
13. Si quiere que los valores diferentes a los valores predeterminados de hello, especifique valores para propiedades de Hola. Hello propiedades para la publicación de Azure están en hello **implementación** sección y también puede tener parámetros de MSBuild tooset. Por ejemplo, en un proyecto de servicio de nube, toospecify una configuración del servicio distinto de "Nube", establezca demasiado parámetros de MSbuild hello`/p:TargetProfile=[YourProfile]` donde *[YourProfile]* coincide con un archivo de configuración de servicio con un nombre como ServiceConfiguration. *YourProfile*.cscfg.
    
     Hello tabla siguiente muestran las propiedades disponibles Hola Hola **implementación** sección:
    
    | Propiedad | Valor predeterminado |
    | --- | --- |
    | Permitir certificados que no son de confianza |Si el valor es false, los certificados SSL deben estar firmados por una entidad de certificación raíz. |
    | Permitir actualización |Permite Hola implementación tooupdate una implementación existente en lugar de crear uno nuevo. Conserva la dirección IP de Hola. |
    | No eliminar |Si el valor es true, no sobrescriba una implementación no relacionada existente (la actualización está permitida). |
    | Ruta de acceso tooDeployment configuración |Hola ruta tooyour .pubxml archivo para una aplicación web, toohello relativa de carpeta de raíz del repositorio de Hola. Se ignora para los servicios en la nube. |
    | Entorno de implementación de SharePoint |Hola igual que el nombre del servicio de Hola. |
    | Entorno de implementación de Azure |Hola aplicación o en la nube nombre de servicio web. |
14. Llegados a este punto, la compilación debería haber finalizado correctamente.
    
     ![][28]
15. Si hace doble clic en nombre de la compilación de hello, Visual Studio muestra un **resumen de la compilación**, incluidos los resultados de pruebas de asociados proyectos de prueba unitaria.
    
     ![][29]
16. Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), puede ver implementación Hola asociado en hello **implementaciones** pestaña cuando se selecciona Hola entorno de ensayo.
    
     ![][30]
17. Examinar dirección URL del sitio tooyour. Para una aplicación web, sólo tiene que elegir hello **examinar** botón en hello portal. Para un servicio de nube, elija dirección URL de Hola Hola **vista rápida** sección de hello **panel** página que muestra el entorno de ensayo de Hola.
    
    Las implementaciones de integración continua para servicios en la nube están publicados toohello el entorno de ensayo de forma predeterminada. Puede cambiar esta configuración hello **entorno del servicio de nube alternativo** propiedad demasiado**producción**. Aquí es donde es la dirección URL del sitio de hello en la página del panel del servicio de nube de Hola.
    
    ![][31]
    
    Una nueva pestaña de explorador abrirá el sitio de la ejecución de tooreveal.
    
    ![][32]
18. Si realiza otros cambios tooyour proyecto, desencadenador más se compila y se acumularán varias implementaciones. Hola más reciente uno está marcado como activo.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: Nueva implementación de una compilación anterior
Este paso es opcional. En Hola portal de Azure clásico, elija una implementación anterior y elija **volver a implementar** toorewind su tooan de sitio anteriormente en el repositorio. Tenga en cuenta que esto desencadenará una nueva compilación en TFS y creará una nueva entrada en el historial de implementaciones.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: cambiar la implementación de producción de hello
Cuando esté listo, puede promover Hola ensayo toohello entorno de producción eligiendo **intercambiar** Hola portal de Azure clásico. entorno de ensayo de Hello recién implementado es tooProduction promocionada y entorno de producción de hello anterior, si existe, se convierte en un entorno de ensayo. Hola implementación activa puede ser diferente para entornos de ensayo y producción de hello, pero el historial de implementación de Hola de compilaciones recientes es Hola igual independientemente del entorno.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: Implementación desde una bifurcación de trabajo.
Al usar Git, normalmente realizar cambios en una bifurcación de trabajo e integrar en la bifurcación principal de hello cuando el desarrollo de su alcance un estado finalizado. Durante la fase de desarrollo de Hola de un proyecto, podrá desea toobuild e implementar tooAzure de bifurcación de trabajo de Hola.

1. En **Team Explorer**, elija hello **inicio** botón y, a continuación, elija hello **bifurcaciones** botón.
   
    ![][40]
2. Elija hello **nueva bifurcación** vínculo.
   
    ![][41]
3. Especificar nombre de saludo de la bifurcación de hello, como "trabajando" y elegir **crear la bifurcación**. De esta forma se crea una nueva bifurcación local.
   
    ![][42]
4. Publicar bifurcación Hola. Elija el nombre de rama hello en **bifurcaciones se anuló la publicación**y elija **publicar**.
   
    ![][44]
5. De forma predeterminada, solo cambia el desencadenador de bifurcación principal toohello una compilación continua. tooset una compilación continua de una bifurcación de trabajo, elija hello **compilaciones** página **Team Explorer**y elija **Editar definición de compilación**.
6. Abra hello **configuración del origen de** ficha. En **supervisan ramas para la integración continua y compilación**, elija **haga clic aquí tooadd una nueva fila**.
   
    ![][47]
7. Especificar la rama de hello que haya creado, tales como refs o cabezales de trabajo.
   
    ![][48]
8. Realizar un cambio en el código de hello, menú contextual abierto Hola Hola cambiado archivo y, a continuación, elija **confirmar**.
   
    ![][43]
9. Elija hello **confirmaciones no sincronizadas** de vínculo y elija hello **sincronización** botón o hello **Push** hello toocopy de vínculo cambia toohello copia de rama de trabajo de hello en Visual Studio Servicios del equipo.
   
   ![][45]
10. Navegue toohello **compilaciones** ver y buscar compilación Hola que simplemente se obtuvo desencadena de rama de trabajo de Hola.

## <a name="next-steps"></a>Pasos siguientes
toolearn más sugerencias sobre cómo usar Git con Visual Studio Team Services, consulte [desarrollar y compartir su código de Git con Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) y para obtener información sobre el uso de un repositorio Git que no está administrado por toopublish de Visual Studio Team Services tooAzure, consulte [tooAzure servicio de aplicaciones de la implementación continua](../app-service-web/app-service-continuous-deployment.md). Para obtener más información sobre Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
