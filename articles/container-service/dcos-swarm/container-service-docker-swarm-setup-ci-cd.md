---
title: aaaCI/CD con conjunto y el servicio de contenedor de Azure | Documentos de Microsoft
description: "Usar el servicio de contenedor de Azure con Docker Swarm, un registro de contenedor de Azure y Visual Studio Team Services toodeliver continuamente una aplicación de .NET Core contenedor múltiples"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Swarm, Azure, Visual Studio Team Services, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>Total de elementos de configuración/CD canalización toodeploy una aplicación de contenedor múltiples en el servicio de contenedor de Azure con Docker Swarm con Visual Studio Team Services

Uno de Hola mayores desafíos cuando desarrollo de aplicaciones modernas de nube de Hola se toodeliver capaz de estas aplicaciones continuamente. En este artículo, obtenga información acerca de cómo crear tooimplement una integración completa continua y la canalización de implementación (CI/CD) con el servicio de contenedor de Azure con Docker Swarm, registro de contenedor de Azure y Visual Studio Team Services y administración de versiones.

Este artículo se basa en una aplicación sencilla, disponible en [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), desarrollada con ASP.NET Core. aplicación Hello se compone de cuatro servicios diferentes: tres web API y front-end uno web:

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

el objetivo de Hello es toodeliver esta aplicación continuamente en un clúster de Docker Swarm, mediante Visual Studio Team Services. Hola siguiente ilustración, detalles de esta canalización de la entrega continua:

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Aquí es una breve explicación de los pasos de hello:

1. Cambios de código están confirmados toohello repositorio de código fuente (aquí, GitHub) 
2. GitHub desencadena una compilación en Visual Studio Team Services. 
3. Visual Studio Team Services obtiene la versión más reciente de Hola de orígenes de Hola y compila todas las imágenes de Hola que componen la aplicación hello 
4. Visual Studio Team Services inserta cada registro de Docker de tooa imágenes creado con el servicio de registro de contenedor de Azure de Hola 
5. Visual Studio Team Services desencadena una nueva versión. 
6. versión de Hola ejecuta algunos comandos mediante SSH en el nodo principal del clúster de servicio de hello contenedor de Azure 
7. Conjunto de docker en hello clúster extrae Hola versión más reciente de imágenes de Hola 
8. nueva versión de la aplicación hello de Hola se implementa con Docker Compose 

## <a name="prerequisites"></a>Requisitos previos

Antes de iniciar este tutorial, necesita hello toocomplete siguientes tareas:

- [Crear un clúster de Swarm en Azure Container Service (servicio Contenedor de Azure)](container-service-deployment.md)
- [Conectar con el clúster de conjunto de hello en el servicio de contenedor de Azure](../container-service-connect.md)
- [Crear una instancia de Azure Container Registry](../../container-registry/container-registry-get-started-portal.md)
- [Crear una cuenta y un proyecto de equipo de Visual Studio Team Services](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Bifurcar hello GitHub repositorio tooyour cuenta de GitHub](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

También se necesita una máquina Ubuntu (14.04 o 16.04) que tenga instalado Docker. Este equipo se utiliza Visual Studio Team Services durante Hola compilar y procesos de la versión. Una manera de toocreate esta máquina es la imagen de hello toouse disponible en hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Paso 1: Configuración de la cuenta de Visual Studio Team Services 

En esta sección, configurará su cuenta de Visual Studio Team Services.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Configuración de un agente de compilación de Linux de Visual Studio Team Services

imágenes de Docker toocreate e inserción que generación estas imágenes en un registro de contenedor de Azure desde un Visual Studio Team Services, deberá tooregister un agente de Linux. Dispone de estas opciones de instalación:

* [Implementar un agente en Linux](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Usar el agente de Docker toorun Hola VSTS](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Instalar extensión de Docker integración VSTS Hola

Microsoft proporciona una extensión VSTS toowork con Docker en la compilación y la versión de procesos. Esta extensión está disponible en hello [Marketplace de VSTS](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Haga clic en **instalar** tooadd esta cuenta VSTS tooyour de extensión:

![Instalar Hola integración del Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Se le preguntará la cuenta VSTS tooyour tooconnect con sus credenciales. 

### <a name="connect-visual-studio-team-services-and-github"></a>Conexión de Visual Studio Team Services y GitHub

Configure una conexión entre el proyecto de VSTS y su cuenta de GitHub.

1. En el proyecto de Visual Studio Team Services, haga clic en hello **configuración** icono en la barra de herramientas de Hola y seleccione **Services**.

    ![Visual Studio Team Services: conexión externa](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Hola izquierda, haga clic en **nuevo extremo de servicio** > **GitHub**.

    ![Visual Studio Team Services: GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. Haga clic en tooauthorize VSTS toowork con su cuenta de GitHub, **Authorize** y siga el procedimiento de hello en la ventana de Hola que se abre.

    ![Visual Studio Team Services: autorización a GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>Conectar del registro VSTS tooyour contenedor de Azure y Azure contenedor servicio de cluster Server

últimos pasos de Hello antes de obtener en la canalización de CI/CD Hola son del registro de tooconfigure conexiones externas tooyour contenedor y el clúster Docker Swarm en Azure. 

1. Hola **servicios** la configuración del proyecto de Visual Studio Team Services, agrega un extremo de servicio de tipo **Docker registro**. 

2. En la ventana emergente de Hola que se abre, escriba Hola URL y las credenciales de Hola de seguridad del registro de contenedor de Azure.

    ![Visual Studio Team Services: Docker Registry](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Para clúster Docker Swarm hello, agregue un punto de conexión de tipo **SSH**. A continuación, escriba la información de conexión de SSH de Hola de su clúster de conjunto.

    ![Visual Studio Team Services: SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

Toda la configuración de Hola se realiza ahora. En pasos de hello, crear canalización de CI/CD de Hola que crea e implementa el clúster de Docker Swarm de hello application toohello. 

## <a name="step-2-create-hello-build-definition"></a>Paso 2: Crear la definición de compilación de Hola

En este paso, debe configurar una definitionfor de compilación del proyecto VSTS y definir flujo de trabajo de compilación de Hola para las imágenes de contenedor

### <a name="initial-definition-setup"></a>Configuración de la definición inicial

1. toocreate una definición de compilación, conectar tooyour del proyecto de Visual Studio Team Services y haga clic en **de compilación y la versión**. 

2. Hola **las definiciones de compilación** sección, haga clic en **+ nuevo**. Seleccione hello **vacía** plantilla.

    ![Visual Studio Team Services: definición de nueva compilación](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. Configurar la nueva compilación de hello con un origen de repositorio de GitHub, verificación **integración continua**y seleccione Hola agente cola que se ha registrado el agente de Linux. Haga clic en **crear** toocreate Hola definición de compilación.

    ![Visual Studio Team Services: creación de la definición de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. En hello **definiciones de compilación** página, primero abra hello **repositorio** pestaña y configurar la bifurcación de Hola de hello compilación toouse del proyecto de MyShop Hola que creó en los requisitos previos de Hola. Asegúrese de que selecciona *acs documentos* como hello **rama predeterminada**.

    ![Visual Studio Team Services: configuración del repositorio de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. En hello **desencadenadores** pestaña, configure Hola compilación toobe desencadena después de cada confirmación. Seleccione **Integración continua** y **Batch changes** (Cambios en lote).

    ![Visual Studio Team Services: configuración del desencadenador de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Definir el flujo de trabajo de compilación de Hola
pasos de Hello definen flujo de trabajo de compilación de Hola. Hay cinco toobuild de imágenes de contenedor para hello *MyShop* aplicación. Cada imagen se basa en hello que dockerfile ubicado en carpetas de proyecto de hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

Necesita dos pasos de Docker tooadd para cada imagen, una imagen de hello toobuild y una imagen de hello toopush en el registro de contenedor de Azure Hola. 

1. Haga clic en un paso en el flujo de trabajo de compilación de hello, tooadd **+ agregar el paso de compilación** y seleccione **Docker**.

    ![Visual Studio Team Services: adición de pasos de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Para cada imagen, configure un paso que usa hello `docker build` comando.

    ![Visual Studio Team Services: compilación de Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Operación de compilación para hello, seleccione el registro de contenedor de Azure, hello **crear una imagen** hello Dockerfile que define cada imagen y acción. Conjunto hello **contexto de la creación** como hello Dockerfile directorio raíz y definir hello **nombre de la imagen**. 
    
    Como se muestra en hello anterior pantalla, inicie nombre de la imagen de hello con hello URI de seguridad del registro de contenedor de Azure. (También puede usar una etiqueta de hello tooparameterize variables de compilación de imagen de hello, como identificador de compilación de hello en este ejemplo).

3. Para cada imagen, configurar un segundo paso que usa hello `docker push` comando.

    ![Visual Studio Team Services: inserción de Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Para la operación de inserción de hello, seleccione el registro de contenedor de Azure, hello **insertar una imagen** acción y escriba hello **nombre de imagen** que se generó en el paso anterior de Hola.

4. Después de configurar compilación hello e insertar pasos para cada una de las imágenes de cinco Hola, agregar que flujo de trabajo de generación de dos pasos más en Hola.

    a. Una tarea de línea de comandos que usa un Hola de bash script tooreplace *BuildNumber* aparición en el archivo de docker compose.yml de hello con hello actual generar Id. Vea Hola después de la pantalla para obtener más información.

    ![Visual Studio Team Services: actualización de archivo de Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Una tarea que quita Hola actualiza redactar archivo como un artefacto de compilación para que se puedan utilizar en la versión de Hola. Vea Hola después de la pantalla para obtener más información.

    ![Visual Studio Team Services: publicación del archivo de Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Haga clic en **Guardar** y asigne un nombre a la definición de compilación.

## <a name="step-3-create-hello-release-definition"></a>Paso 3: Crear definición de la versión de Hola

Visual Studio Team Services le permite demasiado[administrar versiones a través de entornos](https://www.visualstudio.com/team-services/release-management/). Puede habilitar la implementación continua toomake seguro de que la aplicación se implementa en los entornos diferentes (por ejemplo, desarrollo, prueba, el entorno de preproducción y producción) en una forma sencilla. Puede crear un nuevo entorno que representa el clúster de Docker Swarm de Azure Container Service.

![Visual Studio Team Services - versión tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configuración inicial de la versión.

1. toocreate una definición de la versión, haga clic en **versiones** > **+ de la versión**

2. origen de artefacto de hello tooconfigure, haga clic en **artefactos** > **vincular un origen de artefacto**. A continuación, vincular esta nueva compilación de toohello de definición de versión que ha definido en el paso anterior de Hola. Al hacerlo, el archivo de docker compose.yml de hello está disponible en proceso de lanzamiento de Hola.

    ![Visual Studio Team Services: artefactos de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. desencadenador de versión de hello tooconfigure, haga clic en **desencadenadores** y seleccione **implementación continua**. Los desencadenadores de Hola de conjunto de Hola mismo origen de artefacto. Este valor garantiza que una nueva versión se inicia en cuanto Hola generación finalice correctamente.

    ![Visual Studio Team Services: desencadenadores de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Definir el flujo de trabajo de hello versión

flujo de trabajo de Hello versión se compone de dos tareas que agregue.

1. Configurar un Hola de copia de tarea toosecurely crear archivo tooa *implementar* carpeta hello Docker Swarm nodo maestro, mediante conexión de SSH de Hola que configuró anteriormente. Vea Hola después de la pantalla para obtener más información.

    ![Visual Studio Team Services: SCP de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. Configurar un segundo tooexecute de tarea un toorun de comandos de bash `docker` y `docker-compose` comandos en el nodo principal de Hola. Vea Hola después de la pantalla para obtener más información.

    ![Visual Studio Team Services: bash de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    comando de Hello ejecutado en uso principal de Hola Hola CLI de Docker y Hola Hola de toodo de CLI de Docker Compose siguientes tareas:

    - Registro de inicio de sesión toohello contenedor de Azure (usa tres variab'les de compilación que se definen en hello **Variables** ficha)
    - Definir hello **DOCKER_HOST** toowork variable con el punto de conexión de hello conjunto (: 2375)
    - Navegue toohello *implementar* carpeta Hola delante de la tarea de copia de seguridad que creó y que contiene el archivo de hello compose.yml docker 
    - Ejecutar `docker-compose` comandos que extraen nuevas imágenes de hello, detener los servicios de hello, quitar servicios de Hola y crear contenedores de Hola.

    >[!IMPORTANT]
    > Como se muestra en hello delante de la pantalla, deje hello **producirá un error en STDERR** casilla desactivada. Se trata de una opción importante, porque `docker-compose` imprime varios mensajes de diagnóstico, como los contenedores son deteniéndose o eliminando, en la salida de error estándar de Hola. Si activa la casilla de verificación de Hola, Visual Studio Team Services informa de que se producen errores durante la versión de hello, incluso si todo funciona correctamente.
    >
3. Guarde esta nueva definición de versión.


>[!NOTE]
>Esta implementación incluye algún tiempo de inactividad porque estamos detener servicios antiguo hello y ejecuta Hola de nuevo. Es posible tooavoid realizando una implementación de verde azulado.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>Paso 4 Probar Hola CI/CD canalización

Ahora que ha terminado con la configuración de hello, es hora tootest esta nueva canalización de CI/CD. Hola tootest de manera más sencilla es tooupdate Hola origen código y confirmación Hola cambia en el repositorio de GitHub. Unos pocos segundos después de insertar código de hello, verá una nueva compilación que se ejecuta en Visual Studio Team Services. Una vez completada correctamente, una nueva versión se activará e implementará la nueva versión de hello de la aplicación hello en clúster del servicio de contenedor de Azure de Hola.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información acerca de elementos de configuración/CD con Visual Studio Team Services, vea hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).
