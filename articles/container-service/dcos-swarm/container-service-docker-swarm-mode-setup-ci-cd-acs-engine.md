---
title: aaaCI/CD con motor del servicio de contenedor de Azure y el modo Swarm | Documentos de Microsoft
description: "Usar el motor del servicio de contenedor de Azure con Docker Swarm modo, un registro de contenedor de Azure y Visual Studio Team Services toodeliver continuamente una aplicación de .NET Core contenedor múltiples"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, contenedores, microservicios, Swarm, Azure, Visual Studio Team Services, DevOps, ACS Engine
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>Completa CI/CD canalización toodeploy una aplicación de contenedor múltiples en el servicio de contenedor de Azure con el motor de ACS y el modo de Swarm de Docker mediante Visual Studio Team Services

*En este artículo se basa en [completa/CD de elemento de configuración de canalización toodeploy una aplicación de contenedor múltiples en el servicio de contenedor de Azure con Docker Swarm con Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentación*

Hoy en día, uno de Hola mayores desafíos cuando desarrollo de aplicaciones modernas de nube de Hola se toodeliver capaz de estas aplicaciones continuamente. En este artículo, aprenderá cómo tooimplement una integración completa continua e implementación (CI/CD) canalización utilizando: 
* Azure Container Service Engine con modo Docker Swarm
* Azure Container Registry
* Visual Studio Team Services

Este artículo se basa en una aplicación sencilla, disponible en [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), desarrollada con ASP.NET Core. aplicación Hello se compone de cuatro servicios diferentes: tres web API y front-end uno web:

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

el objetivo de Hello es toodeliver esta aplicación continuamente en un clúster en modo de Docker Swarm, mediante Visual Studio Team Services. Hola siguiente ilustración, detalles de esta canalización de la entrega continua:

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Aquí es una breve explicación de los pasos de hello:

1. Cambios de código están confirmados toohello repositorio de código fuente (aquí, GitHub) 
2. GitHub desencadena una compilación en Visual Studio Team Services. 
3. Visual Studio Team Services obtiene la versión más reciente de Hola de orígenes de Hola y compila todas las imágenes de Hola que componen la aplicación hello 
4. Visual Studio Team Services inserta cada registro de Docker de tooa imágenes creado con el servicio de registro de contenedor de Azure de Hola 
5. Visual Studio Team Services desencadena una nueva versión. 
6. versión de Hola ejecuta algunos comandos mediante SSH en el nodo principal del clúster de servicio de hello contenedor de Azure 
7. Docker Swarm el modo en el clúster de hello extrae la versión más reciente de Hola de imágenes de Hola 
8. se implementa Hola nueva versión de la aplicación hello utilizan la pila de Docker 

## <a name="prerequisites"></a>Requisitos previos

Antes de iniciar este tutorial, necesita hello toocomplete siguientes tareas:

- [Crear un clúster del modo Swarm en Azure Container Service con ACS Engine](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Conectar con el clúster de conjunto de hello en el servicio de contenedor de Azure](../container-service-connect.md)
- [Crear una instancia de Azure Container Registry](../../container-registry/container-registry-get-started-portal.md)
- [Crear una cuenta y un proyecto de equipo de Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Bifurcar hello GitHub repositorio tooyour cuenta de GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> Hola Docker Swarm orchestrator en el servicio de contenedor de Azure utiliza la independiente heredado conjunto. Actualmente, Hola integrado [modo conjunto](https://docs.docker.com/engine/swarm/) (en Docker 1.12 y versiones posteriores) no es un orchestrator admitido en el servicio de contenedor de Azure. Por esta razón, estamos utilizando [motor ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), han contribuido una comunidad [plantilla de inicio rápido](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), o una solución de Docker en hello [Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Paso 1: Configuración de la cuenta de Visual Studio Team Services 

En esta sección, configurará su cuenta de Visual Studio Team Services. Extremos de los servicios de VSTS tooconfigure, en el proyecto de Visual Studio Team Services, haga clic en hello **configuración** icono en la barra de herramientas de Hola y seleccione **Services**.

![Abrir punto de conexión de servicios](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Conexión de Visual Studio Team Services y una cuenta de Azure

Configure una conexión entre el proyecto de VSTS y su cuenta de Azure.

1. Hola izquierda, haga clic en **nuevo extremo de servicio** > **Azure Resource Manager**.
2. tooauthorize VSTS toowork con su cuenta de Azure, seleccione su **suscripción** y haga clic en **Aceptar**.

    ![Visual Studio Team Services: autorización a Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Conexión de Visual Studio Team Services y GitHub

Configure una conexión entre el proyecto de VSTS y su cuenta de GitHub.

1. Hola izquierda, haga clic en **nuevo extremo de servicio** > **GitHub**.
2. Haga clic en tooauthorize VSTS toowork con su cuenta de GitHub, **Authorize** y siga el procedimiento de hello en la ventana de Hola que se abre.

    ![Visual Studio Team Services: autorización a GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>Conectar el clúster de servicio de contenedor de Azure VSTS tooyour

últimos pasos de Hello antes de obtener en la canalización de CI/CD Hola son tooconfigure conexiones externas tooyour Docker Swarm con clústeres en Azure. 

1. Para clúster Docker Swarm hello, agregue un punto de conexión de tipo **SSH**. A continuación, escriba la información de conexión de SSH de Hola de su clúster de conjunto (nodo maestro).

    ![Visual Studio Team Services: SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Toda la configuración de Hola se realiza ahora. En pasos de hello, crear canalización de CI/CD de Hola que crea e implementa el clúster de Docker Swarm de hello application toohello. 

## <a name="step-2-create-hello-build-definition"></a>Paso 2: Crear la definición de compilación de Hola

En este paso, debe configura una definición de compilación para el proyecto VSTS y definir flujo de trabajo de compilación de Hola para las imágenes de contenedor

### <a name="initial-definition-setup"></a>Configuración de la definición inicial

1. toocreate una definición de compilación, conectar tooyour del proyecto de Visual Studio Team Services y haga clic en **de compilación y la versión**. Hola **las definiciones de compilación** sección, haga clic en **+ nuevo**. 

    ![Visual Studio Team Services: definición de nueva compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Seleccione hello **proceso vacío**.

    ![Visual Studio Team Services: nueva definición de compilación vacía](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. A continuación, haga clic en hello **Variables** pestaña y cree dos nuevas variables: **RegistryURL** y **AgentURL**. Pegue los valores de hello de su registro y DNS de agentes de clúster.

    ![Visual Studio Team Services configuración de variables de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. En hello **definiciones de compilación** página, abra hello **desencadenadores** pestaña y configurar la integración continua de hello compilación toouse con bifurcar Hola del proyecto de MyShop Hola que creó en los requisitos previos de Hola. Luego, seleccione **Cambios del lote**. Asegúrese de que selecciona *linux docker* como hello **bifurcar especificación**.

    ![Visual Studio Team Services: configuración del repositorio de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Por último, haga clic en hello **opciones** y a configurar cola Hola predeterminada del agente demasiado**vista previa de Linux hospedadas**.

    ![Visual Studio Team Services: configuración del agente de host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Definir el flujo de trabajo de compilación de Hola
pasos de Hello definen flujo de trabajo de compilación de Hola. En primer lugar, necesita tooconfigure Hola origen del código de hello. toodo él, seleccione **GitHub** y su **repositorio** y **bifurcación** (docker-linux).

![Visual Studio Team Services: configurar origen del código](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Hay cinco toobuild de imágenes de contenedor para hello *MyShop* aplicación. Cada imagen se basa en hello que dockerfile ubicado en carpetas de proyecto de hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

Necesita dos pasos de Docker para cada imagen, una imagen de hello toobuild y una imagen de hello toopush en el registro de hello contenedor de Azure. 

1. Haga clic en un paso en el flujo de trabajo de compilación de hello, tooadd **+ agregar el paso de compilación** y seleccione **Docker**.

    ![Visual Studio Team Services: adición de pasos de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Para cada imagen, configure un paso que usa hello `docker build` comando.

    ![Visual Studio Team Services: compilación de Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Operación de compilación para hello, seleccione el registro de contenedor de Azure, hello **crear una imagen** hello Dockerfile que define cada imagen y acción. Hola de conjunto **Working Directory** como directorio raíz de hello Dockerfile, definir hello **nombre de la imagen**y seleccione **etiqueta más reciente Include**.
    
    Nombre de la imagen de Hello tiene toobe en este formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Reemplace **[NAME]** con el nombre de la imagen de hello:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Para cada imagen, configurar un segundo paso que usa hello `docker push` comando.

    ![Visual Studio Team Services: inserción de Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Para la operación de inserción de hello, seleccione el registro de contenedor de Azure, hello **insertar una imagen** acción, escriba Hola **nombre de la imagen** que está integrado en el paso anterior de Hola y seleccione **incluir la etiqueta más reciente** .

4. Después de configurar compilación hello e insertar pasos para cada una de las imágenes de cinco Hola, agregar que flujo de trabajo de generación de tres pasos más en Hola.

   ![Visual Studio Team Services: adición de una tarea de la línea de comandos](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Una tarea de línea de comandos que usa un Hola de bash script tooreplace *RegistryURL* aparición en el archivo de docker compose.yml de hello con variable de RegistryURL Hola. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services: actualización del archivo de Compose con la URL del Registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Una tarea de línea de comandos que usa un Hola de bash script tooreplace *AgentURL* aparición en el archivo de docker compose.yml de hello con variable de AgentURL Hola.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Una tarea que quita Hola actualiza redactar archivo como un artefacto de compilación para que se puedan utilizar en la versión de Hola. Vea Hola después de la pantalla para obtener más información.

         ![Visual Studio Team Services: publicación de artefacto](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services: publicación del archivo de Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Haga clic en **Guardar & cola** tootest la definición de compilación.

   ![Visual Studio Team Services: guardar y poner en cola](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services: nueva cola](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Si hello **generar** es correcta, deberá toosee esta pantalla:

  ![Visual Studio Team Services: compilación correcta](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>Paso 3: Crear definición de la versión de Hola

Visual Studio Team Services le permite demasiado[administrar versiones a través de entornos](https://www.visualstudio.com/team-services/release-management/). Puede habilitar la implementación continua toomake seguro de que la aplicación se implementa en los entornos diferentes (por ejemplo, desarrollo, prueba, el entorno de preproducción y producción) en una forma sencilla. Puede crear un entorno que represente el clúster del modo Docker Swarm de Azure Container Service.

![Visual Studio Team Services - versión tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configuración inicial de la versión.

1. toocreate una definición de la versión, haga clic en **versiones** > **+ de la versión**

2. origen de artefacto de hello tooconfigure, haga clic en **artefactos** > **vincular un origen de artefacto**. A continuación, vincular esta nueva compilación de toohello de definición de versión que ha definido en el paso anterior de Hola. Después de eso, el archivo de docker compose.yml de hello está disponible en el proceso de lanzamiento de Hola.

    ![Visual Studio Team Services: artefactos de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. desencadenador de versión de hello tooconfigure, haga clic en **desencadenadores** y seleccione **implementación continua**. Los desencadenadores de Hola de conjunto de Hola mismo origen de artefacto. Este valor garantiza que una nueva versión se inicia cuando se complete correctamente la compilación de Hola.

    ![Visual Studio Team Services: desencadenadores de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. las variables de la versión de Hola del tooconfigure, haga clic en **Variables** y seleccione **+ Variable** toocreate tres nuevas variables con información de hello del registro de hello: **docker.username**, **docker.password**, y **docker.registry**. Pegue los valores de hello de su registro y DNS de agentes de clúster.

    ![Visual Studio Team Services: configuración del repositorio de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Como se muestra en la pantalla de bienvenida anterior, haga clic en hello **bloqueo** checkbox en docker.password. Esta configuración es la contraseña de Hola de toorestrict importante.
    >

### <a name="define-hello-release-workflow"></a>Definir el flujo de trabajo de hello versión

flujo de trabajo de Hello versión se compone de dos tareas que agregue.

1. Configurar un Hola de copia de tarea toosecurely crear archivo tooa *implementar* carpeta hello Docker Swarm nodo maestro, mediante conexión de SSH de Hola que configuró anteriormente. Vea Hola después de la pantalla para obtener más información.
    
    Carpeta de origen:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services: SCP de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Configurar un segundo tooexecute de tarea un toorun de comandos de bash `docker` y `docker stack deploy` comandos en el nodo principal de Hola. Vea Hola después de la pantalla para obtener más información.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services: bash de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    comando de Hello ejecutado en el maestro de hello usa Hola CLI de Docker y Hola Hola de toodo de CLI de Docker Compose siguiente las tareas:

    - Inicie sesión en el registro de contenedor de Azure toohello (utiliza tres variables de compilación que se definen en hello **Variables** ficha)
    - Definir hello **DOCKER_HOST** toowork variable con el punto de conexión de hello conjunto (: 2375)
    - Navegue toohello *implementar* carpeta Hola delante de la tarea de copia de seguridad que creó y que contiene el archivo de hello compose.yml docker 
    - Ejecutar `docker stack deploy` comandos que extracción nuevas imágenes de Hola y crean contenedores de Hola.

    >[!IMPORTANT]
    > Como se muestra en la pantalla de bienvenida anterior, deje hello **producirá un error en STDERR** casilla desactivada. Esta opción permite que nos toocomplete Hola versión de vencimiento del proceso demasiado`docker-compose` imprime varios mensajes de diagnóstico, como los contenedores son deteniéndose o eliminando, en la salida de error estándar de Hola. Si activa la casilla de verificación de Hola, Visual Studio Team Services informa de que se producen errores durante la versión de hello, incluso si todo funciona correctamente.
    >
3. Guarde esta nueva definición de versión.

## <a name="step-4-test-hello-cicd-pipeline"></a>Paso 4: Probar la canalización de CI/CD Hola

Ahora que ha terminado con la configuración de hello, es hora tootest esta nueva canalización de CI/CD. Hola tootest de manera más sencilla es tooupdate Hola origen código y confirmación Hola cambia en el repositorio de GitHub. Unos pocos segundos después de insertar código de hello, verá una nueva compilación que se ejecuta en Visual Studio Team Services. Una vez completada correctamente, una nueva versión se desencadena e implementa la nueva versión de hello de la aplicación hello en clúster del servicio de contenedor de Azure de Hola.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información acerca de elementos de configuración/CD con Visual Studio Team Services, vea hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).
* Para obtener más información sobre el motor de ACS, vea hello [repositorio de GitHub de motor de ACS](https://github.com/Azure/acs-engine).
* Para obtener más información acerca del modo de Docker Swarm, vea hello [Docker Swarm información general de modo](https://docs.docker.com/engine/swarm/).
