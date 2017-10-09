---
title: "una aplicación de Azure Service Fabric con integración continua (Team Services) aaaDeploy | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset la integración continua y de implementación para una aplicación de Service Fabric mediante Visual Studio Team Services.  Implementar un clúster de Service Fabric tooa de aplicación en Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Implementar una aplicación con el clúster de Service Fabric tooa CI/CD
Este tutorial es parte tres de una serie y se describe cómo tooset la integración continua y de implementación para una aplicación de Azure Service Fabric con Visual Studio Team Services.  Se necesita una aplicación de Service Fabric existente, la aplicación hello creado en [generar una aplicación .NET](service-fabric-tutorial-create-dotnet-app.md) se utiliza como ejemplo.

En esta parte de la serie de hello, aprenderá cómo:

> [!div class="checklist"]
> * Agregar proyecto de tooyour de control de código fuente
> * Crear una definición de compilación en Team Services
> * Crear una definición de versión en Team Services
> * Implementar y actualizar una aplicación automáticamente

En esta serie de tutoriales, se aprende a:
> [!div class="checklist"]
> * [Crear una aplicación de .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * [Implementar el clúster remoto de hello aplicación tooa](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Configurar CI/CD con Visual Studio Team Services

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar este tutorial:
- Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Instalar Visual Studio de 2017](https://www.visualstudio.com/) e instalar hello **desarrollo Azure** y **ASP.NET y desarrollo web** las cargas de trabajo.
- [Instalar Hola SDK del servicio de Fabric](service-fabric-get-started.md)
- Cree una aplicación de Service Fabric (por ejemplo, [siguiendo este tutorial](service-fabric-tutorial-create-dotnet-app.md)). 
- Cree un clúster de Windows Service Fabric en Azure (por ejemplo, [siguiendo este tutorial](service-fabric-tutorial-create-cluster-azure-ps.md)).
- Cree una [cuenta de Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Descargar la aplicación de ejemplo de Hola votación
Si no se ha generado la aplicación de ejemplo de Hola votación [primera parte de esta serie de tutoriales](service-fabric-tutorial-create-dotnet-app.md), puede descargarlo. En una ventana de comandos, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Preparar un perfil de publicación
Ahora que ya [creó una aplicación](service-fabric-tutorial-create-dotnet-app.md) y tener [implementado Hola aplicación tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), está listo tooset la integración continua.  En primer lugar, prepare un perfil de publicación dentro de la aplicación para su uso por proceso de implementación de Hola que se ejecuta dentro de Team Services.  Hola perfil de publicación debe ser el clúster de hello tootarget configurado que haya creado anteriormente.  Inicie Visual Studio y abra un proyecto de aplicación existente de Service Fabric.  En **el Explorador de soluciones**, haga clic en la aplicación hello y seleccione **publicar...** .

Elija un perfil de destino dentro de su toouse de proyecto de aplicación para el flujo de trabajo de integración continua, por ejemplo en la nube.  Especifique el extremo de conexión de clúster de Hola.  Comprobar hello **actualización Hola aplicación** casilla de verificación para que la aplicación se actualiza para cada implementación de Team Services.  Haga clic en hello **guardar** hipervínculo toosave Hola configuración toohello perfil de publicación y, a continuación, haga clic en **cancelar** cuadro de diálogo de tooclose Hola.  

![Perfil de inserción][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Compartir su repositorio de Git de Team Services nuevo de Visual Studio solución tooa
Compartir los archivos de origen de la aplicación genera tooa el proyecto de equipo en Team Services, por lo que puede generar.  

Crear un nuevo repositorio Git local para el proyecto seleccionando **agregar tooSource Control** -> **Git** en la barra de estado de hello en la esquina derecha inferior de Hola de Visual Studio. 

Hola **Push** ver en **Team Explorer**, seleccione hello **publicar el repositorio de Git** situado bajo **Push tooVisual Studio Team Services**.

![Repositorio Git de inserción][push-git-repo]

Compruebe su correo electrónico y seleccione su cuenta de hello **equipo de servicios de dominio** lista desplegable. Escriba el nombre del repositorio y seleccione **Publicar repositorio**.

![Repositorio Git de inserción][publish-code]

Repositorio de hello al publicar, crea un nuevo proyecto de equipo en su cuenta con hello mismo nombre como repositorio local Hola. repositorio de hello toocreate en un proyecto de equipo existente, haga clic en **avanzadas** siguiente demasiado**repositorio** asigne un nombre y seleccione un proyecto de equipo. Puede ver el código en web Hola seleccionando **verlo en web de hello**.

## <a name="configure-continuous-delivery-with-vsts"></a>Configurar la entrega continua con VSTS
Una definición de compilación de Team Services describe un flujo de trabajo compuesto por una serie de pasos de compilación que se ejecutan de manera secuencial. Crear una definición de compilación que genera un paquete de aplicación de Service Fabric y otros artefactos, el clúster de Service Fabric tooa toodeploy. Obtenga más información sobre las [definiciones de compilación de Team Services](https://www.visualstudio.com/docs/build/define/create). 

Una definición de la versión de Team Services describe un flujo de trabajo que se puede implementar un clúster de tooa del paquete de aplicación. Cuando se usan juntos, Hola definición de compilación y definición de versión ejecute hello flujo de trabajo completo a partir de tooending de archivos de origen con una aplicación en ejecución en el clúster. Obtenga más información sobre las [definiciones de versión](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)de Team Services.

### <a name="create-a-build-definition"></a>Creación de una definición de compilación
Abra un explorador web y navegue tooyour nuevo proyecto de equipo en: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Seleccione hello **compilar & versión** pestaña, a continuación, **compilaciones**, a continuación, **+ nueva definición**.  En **seleccione una plantilla de**, seleccione hello **aplicación de Azure Service Fabric** plantilla y haga clic en **aplicar**. 

![Elegir la plantilla de compilación][select-build-template] 

Hola votos de aplicación contiene un proyecto de .NET Core, por lo que agregue una tarea que restaura las dependencias de Hola. Hola **tareas** visualizarla, seleccione **+ agregar tarea** en la parte inferior de hello izquierda. Buscar en la tarea de línea de comandos de "Línea de comandos" toofind hello, a continuación, haga clic en **agregar**. 

![Agregar tarea][add-task] 

En la nueva tarea hello, escriba "Ejecutar dotnet.exe" en **nombre para mostrar**, "dotnet.exe" en **herramienta**y "restore" en **argumentos**. 

![Nueva tarea][new-task] 

Hola **desencadenadores** ver, haga clic en hello **habilitar este desencadenador** cambie en **integración continua**. 

Seleccione **Guardar & cola** y escriba "Hospedado VS2017" hello **cola del agente**. Seleccione **cola** toomanually iniciar una compilación.  Las compilaciones también se desencadenan después de una inserción o una protección.

toocheck el progreso de compilación, conmutador toohello **compilaciones** ficha.  Cuando haya comprobado que se ejecuta correctamente la compilación de hello, definir una definición de la versión que implementa el clúster de tooa de aplicación. 

### <a name="create-a-release-definition"></a>Creación de una definición de versión  

Hola seleccione **de compilación y la versión** pestaña, a continuación, **versiones**, a continuación, **+ nueva definición**.  En **Crear definición de versión**, seleccione hello **Azure Service Fabric implementación** plantilla de lista de Hola y haga clic en **siguiente**.  Seleccione hello **generar** de origen, compruebe hello **implementación continua** cuadro y haga clic en **crear**. 

Hola **entornos** ver, haga clic en **agregar** toohello derecha de **conexión de clúster**.  Especifique un nombre de conexión de "mysftestcluster", un punto de conexión de clúster de "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" y hello Azure Active Directory o credenciales de certificado para el clúster de Hola. Para las credenciales de Azure Active Directory, definir las credenciales de hello desea toouse tooconnect toohello clúster Hola **nombre de usuario** y **contraseña** campos. Para la autenticación basada en certificados, defina Hola Base64 codificación del archivo de certificado de cliente de Hola Hola **certificado de cliente** campo.  Consulte la ventana emergente de Ayuda de hello en ese campo para obtener información acerca de cómo tooget ese valor.  Si el certificado está protegido por contraseña, Definir contraseña Hola Hola **contraseña** campo.  Haga clic en **guardar** definición de versión de hello toosave.

![Agregar conexión del clúster][add-cluster-connection] 

Haga clic en **Ejecutar en el agente** y seleccione **Hosted VS2017** como **Cola de implementación**. Haga clic en **guardar** definición de versión de hello toosave.

![Ejecutar en el agente][run-on-agent]

Seleccione **+ versión** -> **crear versión** -> **crear** toomanually crear una versión.  Compruebe que se ha realizado correctamente en la implementación de Hola y aplicación hello se ejecuta en el clúster de Hola.  Abra un explorador web y navegue demasiado[http://mysftestcluster.westus.cloudapp.azure.com:19080/explorador/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Observe la versión de la aplicación hello, en este ejemplo es "1.0.0.20170616.3". 

## <a name="commit-and-push-changes-trigger-a-release"></a>Confirmar e insertar cambios y desencadenar una versión
funciona tooverify que Hola canalización de integración continua mediante la comprobación de servicios tooTeam en algunos cambios en el código.    

A medida que escribe el código, los cambios se controlan automáticamente con Visual Studio. Confirmar cambios tooyour repositorio de Git seleccionando Hola pendientes (icono de cambios![Pending][pending]) de la barra de estado de hello en la parte inferior de hello derecha.

En hello **cambios** ver en Team Explorer, agregar un mensaje que describe la actualización y confirmar los cambios.

![Confirmar todo][changes]

Icono de la barra de estado de hello seleccione cambios sin publicar (![anuló la publicación cambios][unpublished-changes]) u Hola vista de sincronización de Team Explorer. Seleccione **Push** tooupdate el código en Team Services o TFS.

![Inserción de los cambios][push]

Insertar Hola cambios tooTeam servicios automáticamente desencadenadores una compilación.  Cuando se complete correctamente la definición de compilación de hello, una versión se crea automáticamente e inicia la actualización de la aplicación hello en clúster de Hola.

toocheck el progreso de compilación, conmutador toohello **compilaciones** ficha **Team Explorer** en Visual Studio.  Cuando haya comprobado que se ejecuta correctamente la compilación de hello, definir una definición de la versión que implementa el clúster de tooa de aplicación.

Compruebe que se ha realizado correctamente en la implementación de Hola y aplicación hello se ejecuta en el clúster de Hola.  Abra un explorador web y navegue demasiado[http://mysftestcluster.westus.cloudapp.azure.com:19080/explorador/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Observe la versión de la aplicación hello, en este ejemplo es "1.0.0.20170815.3".

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Actualizar la aplicación hello
Realizar cambios de código en la aplicación hello.  Guarde y confirmar los cambios de hello, siga los pasos anteriores de Hola.

Una vez que actualice Hola de aplicación hello comienza, puede ver el progreso de la actualización hello en el Explorador de tejido de servicio:

![Service Fabric Explorer][sfx2]

actualización de la aplicación Hello puede tardar varios minutos. Una vez completada la actualización hello, aplicación hello estará en ejecución próxima versión de Hola.  En este ejemplo "1.0.0.20170815.4".

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Agregar proyecto de tooyour de control de código fuente
> * Creación de una definición de compilación
> * Creación de una definición de versión
> * Implementar y actualizar una aplicación automáticamente

Ahora que ha implementado una aplicación y configurado la integración continua, pruebe Hola siguientes:
- [Actualizar una aplicación](service-fabric-application-upgrade.md)
- [Probar una aplicación](service-fabric-testability-overview.md) 
- [Supervisar y diagnosticar](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png